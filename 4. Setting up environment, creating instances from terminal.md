<div align="center">
  <h1>Practical DevOps: SSH Access & AWS CLI Intro</h1>
  <p>Step-by-step guides for connecting to EC2 and automating infrastructure.</p>
</div>

---

<h2 id="part-1">Part 1: Connecting to EC2 from Windows (MobaXterm)</h2>
*Goal: Securely access Linux EC2 instances from a Windows machine.*

### Step-by-Step Setup:
1. **Launch Instance:** Create your instance via AWS Console (e.g., Ubuntu, `t2.micro`).
2. **Key Pair:** 
    * Generate a new Key Pair in AWS. 
    * Choose **.pem** format (recommended for MobaXterm).
    * Download and save it securely (e.g., in `Downloads`).
3. **Install MobaXterm:**
    * Go to [MobaXterm Official Download](https://mobaxterm.mobatek.net/download.html).
    * Choose **Home Edition (Installer)** for the easiest setup.
4. **Connect via SSH:**
    * Open MobaXterm and click **Session > SSH**.
    * **Remote Host:** Enter your instance's Public IP.
    * **Specify Username:** `ubuntu` (for Ubuntu instances).
    * **Advanced SSH Settings:** Check "Use private key" and select the `.pem` file you downloaded.
    * Click **OK** and accept the security fingerprint.

---

<h2 id="part-2">Part 2: AWS CLI & Infrastructure Automation</h2>

### 1. Setup & Authentication
* **Install CLI:** Follow the [AWS CLI Official Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
* **Create Access Keys:**
    * In AWS Console: **User Profile > Security Credentials > Create Access Key**.
    * *Security Note:* Store your Secret Access Key securely. Do not share it.
* **Configure:** Run the following in your terminal:
    ```bash
    aws configure
    ```
    * Enter your Access Key ID, Secret Access Key, and default region (e.g., `us-east-1`).

### 2. Practical Commands (CLI)
* **Verify Installation:** `aws --version`
* **List S3 Buckets:** `aws s3 ls`
* **Create Bucket:** `aws s3 mb s3://<your-unique-bucket-name>`
* **Reference Documentation:** Always consult the [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html) for specific service commands (e.g., `ec2 run-instances`).

---

<h2 id="part-3">Part 3: Infrastructure as Code (Foundations)</h2>

### 1. CloudFormation Templates (CFT)
* **Concept:** Use JSON/YAML files to define infrastructure.
* **How to use:** 
    * Find templates in the [AWS CloudFormation GitHub Repo](https://github.com/aws-samples/aws-cloudformation-templates).
    * In the AWS Console, go to **CloudFormation > Create Stack > With new resources > Upload template**.

### 2. Python Automation (Boto3)
* **Concept:** Use Python to interact with AWS APIs directly.
* **Resources:** Check the [Boto3 Documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html).
* **Basic Script Logic:**
    ```python
    import boto3
    ec2 = boto3.client('ec2')
    instances = ec2.describe_instances()
    print(instances)
    ```

---

### 💡 DevOps Assignment (Homework)
1. **Install AWS CLI** on your local machine.
2. **Authenticate** using your IAM User Access Keys.
3. **Complete a task via Terminal:** Create an S3 bucket or list your EC2 instances using the CLI instead of the website.
4. **Read the Docs:** Search for the `run-instances` command in the [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/reference/ec2/run-instances.html) and understand the required parameters (Image ID, Instance Type, Key Name).
