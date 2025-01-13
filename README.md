# Cloud-Native Website Deployment with AWS

This project demonstrates how to deploy a cloud-native, secure, and scalable static website using various AWS services, including Route 53, CloudFront, S3, Certificate Manager, and CodePipeline. The project automates deployment for a seamless experience and provides HTTPS support for a domain and subdomain.

---

## **Project Overview**

In this project, I deployed a static HTML website on AWS with the following features:
- A root domain (`oxxr.net`) that redirects traffic to a subdomain (`www.oxxr.net`).
- HTTPS-enabled access using **Amazon CloudFront** and **AWS Certificate Manager**.
- Automated deployment using **AWS CodePipeline**.
- Scalable and cost-effective hosting via **Amazon S3**.
- Domain registration and traffic routing through **AWS Route 53**.

This README explains the step-by-step implementation of the project.

---

## **Architecture**

The architecture consists of:
1. **Amazon Route 53**: For domain registration (`oxxr.net`) and DNS routing.
2. **Amazon S3**: To host the static website (subdomain) and redirect the root domain.
3. **AWS Certificate Manager (ACM)**: For public SSL/TLS certificates to enable HTTPS.
4. **Amazon CloudFront**: For secure, fast, and global content delivery.
5. **AWS CodePipeline**: To automate the deployment process.

---

## **Implementation Steps**

### 1. **Create and Register the Domain**
- Registered the domain `oxxr.net` via **AWS Route 53**.
- Configured a hosted zone for DNS management.
- Note: Domain registration incurs charges, which I am currently discussing with AWS Support to waive.

### 2. **Request a Public Certificate**
- Requested an SSL/TLS certificate via **AWS Certificate Manager** for both `oxxr.net` and `www.oxxr.net`.
- Validated the certificate using DNS records provided by ACM.

### 3. **Host the Website with Amazon S3**
#### Subdomain Bucket:
- Created an S3 bucket named `www.oxxr.net` to host the website.
- Enabled static website hosting and uploaded the HTML files.

#### Root Domain Bucket:
- Created another S3 bucket named `oxxr.net` for redirecting requests.
- Configured the bucket to redirect all requests from `oxxr.net` to `www.oxxr.net`.

### 4. **Enable HTTPS with Amazon CloudFront**
#### Subdomain Distribution:
- Created a **CloudFront distribution** for `www.oxxr.net`:
  - Used the subdomain bucket as the origin.
  - Attached the public certificate from ACM to enable HTTPS.

#### Root Domain Distribution:
- Created another **CloudFront distribution** for `oxxr.net`:
  - Set the origin as the redirect bucket.
  - Attached the public certificate to enable HTTPS for the root domain redirect.

### 5. **Route DNS Traffic via Route 53**
- Updated Route 53 hosted zones to route traffic for both domains:
  - Added an **A record** (alias) pointing `www.oxxr.net` to the subdomain CloudFront distribution.
  - Added an **A record** (alias) pointing `oxxr.net` to the root domain CloudFront distribution.

### 6. **Automate Deployment with AWS CodePipeline**
- Set up **AWS CodePipeline** for CI/CD:
  - Configured the pipeline's source stage to use the S3 bucket where the website files are stored.
  - Enabled versioning on the source bucket to manage file updates.
  - Skipped the build stage as this is a static website deployment.
  - Deployed the website automatically whenever changes are made to the source bucket.

---

## **Key AWS Services Used**
- **Route 53**: For domain registration and DNS routing.
- **S3**: For static website hosting and redirection.
- **Certificate Manager**: For free SSL/TLS certificates.
- **CloudFront**: For secure, global content delivery.
- **CodePipeline**: For automating the deployment process.

---

## **Challenges Faced**
1. **Domain Registration Costs**:
   - Encountered a $25 charge for domain registration, which I am discussing with AWS Support for potential reimbursement.
   
2. **SSL/TLS Certificate Validation**:
   - Required careful DNS configuration for validation.
   
3. **CloudFront Configuration**:
   - Ensuring both distributions (root and subdomain) worked seamlessly with HTTPS and redirects.

---

## **Project Workflow**

1. A user accesses `oxxr.net` or `www.oxxr.net` via a browser.
2. **Route 53** routes the traffic to the appropriate CloudFront distribution.
3. CloudFront serves the content securely over HTTPS:
   - `oxxr.net` requests are redirected to `www.oxxr.net`.
   - `www.oxxr.net` serves the static website hosted on S3.
4. Updates to the website are deployed automatically via **CodePipeline**, ensuring seamless integration and delivery.

---

## **References**
- [AWS Route 53: Getting Started with CloudFront](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/getting-started-cloudfront-overview.html#getting-started-cloudfront-domain-name)
- [AWS Route 53: Routing to a CloudFront Distribution](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-cloudfront-distribution.html)

---

## **Conclusion**
This project demonstrates how to build and deploy a secure, scalable, and automated static website using AWS services. By leveraging AWS's robust tools, I was able to achieve a cloud-native architecture that ensures high performance, reliability, and ease of deployment.

Feel free to explore the code and contribute: [GitHub Repository](https://github.com/v-i-k-a-s-1-7/single-server-deployment.git)
