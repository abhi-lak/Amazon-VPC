# Amazon S3 Static Website Hosting

## Project Overview

In this project, I created an Amazon S3 bucket to store website files and host a static website. The purpose was to understand how S3 object storage works, how static website hosting is configured, and how access permissions can be managed using Access Control Lists (ACLs) and bucket policies.

## Tools and Concepts

- Amazon S3
- S3 bucket creation and object storage
- Static website hosting
- S3 website endpoint
- Access Control Lists (ACLs)
- Bucket policies and IAM-style permissions
- Public access configuration

I learned how to upload website files, enable static website hosting, configure public read access, troubleshoot a 403 Forbidden error, and use a bucket policy to protect an important website file from deletion.

## Time, Challenges, and Outcomes

The project took approximately **30 minutes** to complete. The most challenging part was troubleshooting the 403 Forbidden error and configuring the correct access permissions. The most rewarding part was seeing the website become accessible through its S3 website endpoint and learning how S3 permissions can be used to control access to website files.

---

## 1. Creating an S3 Bucket

### What I did

I opened the Amazon S3 service in the AWS Management Console and created a bucket to store the files for my static website.

### Time taken

Creating the bucket took approximately **5 minutes**.

### Region selection

I selected **Asia Pacific (Mumbai) – ap-south-1** because it was geographically close to me.

### Understanding bucket-name uniqueness

S3 general-purpose bucket names must be unique across the AWS partition. This means another AWS account in the same partition cannot create a bucket with the same name while my bucket exists. If I delete the bucket, its name may become available for someone else to use.

---

## 2. Uploading Website Files to S3

### What I did

I downloaded the HTML file for the website and a ZIP archive containing the website images. I then uploaded the required files to my S3 bucket.

### Files uploaded

I uploaded the website's HTML file and the folder containing the images used by the website.

### How the files work together

The HTML file provides the structure and content of the website. The image files supply the visual content displayed on the page. The HTML file must refer to the images using the correct paths so that they load successfully.

---

## 3. Enabling Static Website Hosting

### What I did

I configured my S3 bucket for static website hosting so that visitors could access the website through a web browser.

### What is website hosting?

Website hosting is a service that stores website files on an internet-connected server and makes them available to visitors through a web browser.

### How I enabled website hosting

I opened my S3 bucket, went to the **Properties** tab, and located the **Static website hosting** section. I selected **Edit**, enabled static website hosting, chose the option to host a static website, and entered `index.html` as the index document. I saved the settings and used the S3 website endpoint provided by AWS to access the website.

### Understanding Access Control Lists (ACLs)

An Access Control List (ACL) is a mechanism for granting basic access permissions to an S3 bucket or an individual object. Depending on the bucket's Object Ownership configuration, ACLs can be used to grant permissions such as read access to specified AWS accounts or predefined groups.

---

## 4. Understanding the S3 Website Endpoint

### What is a bucket website endpoint URL?

When static website hosting is enabled, Amazon S3 provides a website endpoint URL. This is the web address visitors use to open the static website hosted in the bucket. The endpoint is specific to the bucket and AWS Region.

### What I saw when I tested the endpoint

When I first opened the bucket website endpoint, I received an **Access Denied (403 Forbidden)** error. This happened because the website files were not yet publicly readable. I needed to configure the appropriate S3 access permissions before visitors could load the website.

---

## 5. Making the Website Publicly Accessible

### What I did

I updated the S3 bucket's public access configuration and used the **ACL** settings to grant public read access to the website objects. This allowed visitors to retrieve the files needed to display the website.

### How I resolved the 403 Forbidden error

I resolved the 403 Forbidden error by changing the ACL permissions for the website objects. I granted the **Everyone (public access)** group read permission. After applying the changes, I opened the S3 website endpoint again and confirmed that the website was accessible.

> **Security note:** Public read access makes the relevant website objects available to anyone on the internet. It should only be enabled for files that are intended to be public. The bucket's Block Public Access settings and Object Ownership configuration must also allow the chosen ACL-based approach.

### Project outcome

The static website was successfully hosted on Amazon S3 and could be opened through its website endpoint.

---

## 6. Protecting `index.html` with a Bucket Policy

### What I did in this extension

I configured an S3 bucket policy to protect the `index.html` file from deletion. The policy explicitly denies the `s3:DeleteObject` action for that object. I then tested the policy by attempting to delete the file.

### What is a bucket policy?

A bucket policy is a JSON-based resource policy attached to an S3 bucket. It defines which principals can or cannot perform specified actions on the bucket and its objects.

Bucket policies provide centralized and detailed access control at the bucket level. ACLs, in comparison, provide a more limited way to grant basic permissions to buckets and objects.

### What my bucket policy does

My bucket policy explicitly denies the `s3:DeleteObject` action on the `index.html` object. An explicit deny takes precedence over an allow, so the object cannot be deleted while this policy applies.

I tested the policy by attempting to delete `index.html` from the S3 bucket. The operation returned an **Access Denied** error, confirming that the policy prevented the deletion.

---

## Key Learnings

Through this project, I learned how to create an Amazon S3 bucket, upload website files, enable static website hosting, and access a website through an S3 website endpoint. I also learned how ACLs can grant public read access to website objects, how to troubleshoot a 403 Forbidden error, and how bucket policies can enforce restrictions such as preventing the deletion of `index.html`. Overall, the project strengthened my understanding of AWS cloud storage, static website deployment, access management, and basic cloud security.
