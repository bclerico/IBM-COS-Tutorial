# Using IBM Cloud Object Storage from a Command Line Interface
This tutorial provides an overview of setting up and using IBM COS from a Command Line Interface.
1. [Prerequisites and Assumptions)](#pre-reqs)
1. [Download and install the AWS CLI package](#dwnl_awscli)
1. [Create an instance of the IBM COS Service](#create_cos)
1. [Create and Save Service Credentials](#create_creds)
1. [Create a Bucket](#create_bucket)
1. Upload Files to the bucket
1. Configure the AWS CLI with IBM COS credentials
1. Create LM (lazy man) script
1. Run scenarios (prefixes, cp, sync, static web hosting, presigned URIs, getting files on S3, etc.)


## <a name="pre-reqs">1. Prerequisites and Assumptions</a>
The section documents the prerequisites and assumptions for this tutorial.
1. ASSUMPTION: You are running on MAC/OS.  All examples are demonstrated on MAC/OS, however these instructions can be easily adapted to other platforms.

1. REQUIRED: Python 2 version 2.6.5+ or Python 3 version 3.3+. Verify your Python version in a terminal window with the following command:

   `$ python --version`

   If you need to install or upgrade Python [you can find the downloads here](https://www.python.org/downloads/).

1. REQUIRED: IBM Cloud Account.  [Sign up for an account here](https://console.bluemix.net/registration/).

## <a name="dwnl_awscli">2. Download and Install the AWS CLI package</a>

**Note:** Complete instructions and additional help can be found in the [AWS CLI User Guide](https://docs.aws.amazon.com/cli/latest/userguide/installing.html).  The following instructions are suitable for most installations.
1. Download the AWS Bundled Installer by [clicking here](https://s3.amazonaws.com/aws-cli/awscli-bundle.zip).  As an alternative you can use CURL to download:

   `$ curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"`

1. Locate the downloaded package and unzip it by double-clicking on it.  As an alternative you can use UNZIP:

   `$ unzip awscli-bundle.zip`

1. Run the *install* executable:

   `sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws`

   **Note:** The MAC/OS installer places the AWS CLI files in */usr/local/aws* and creates the symlink *aws* in */usr/local/bin*. Should the need to uninstall or remove the AWS CLI arise you can simply remove these files:

   `$ sudo rm -rf /usr/local/aws`

   `$ sudo rm /usr/local/bin/aws`

1. Verify that the installation succeeded:

   `$ aws --version`

## <a name="create_cos">3. Create an instance of the IBM COS Service</a>

1. Login into the IBM Cloud console, navigate to the Catalog, search for Object Storage, and click on it.

   ![Login to IBM Cloud, navigate to the Catalog, search for Object Storage, select plan](https://user-images.githubusercontent.com/8126772/40881704-8b193210-669b-11e8-9561-60c1751c3949.JPG)

1. The *Lite* plan is automatically selected for you. Click **Create**.

   ![Click Create](https://user-images.githubusercontent.com/8126772/40881777-fd0b42da-669d-11e8-8578-afbed80d57cf.JPG)

## <a name="create_creds">4. Create and Save Service Credentials</a>

In order to access the COS Service from a command line interface you must be able to assert that you have the authority to access the content that COS is managing. This is done through the use of *Service credentials*.

1. Once the Service is provisioned click on *Service credentials*.

   ![Click on Service Credentials](https://user-images.githubusercontent.com/8126772/40881960-bfe534ce-66a2-11e8-8ace-1cb609f625eb.JPG)

1. Click on *New credential*.

   ![Click on New Credential](https://user-images.githubusercontent.com/8126772/40882016-f2cfa580-66a3-11e8-9b8f-db44364f0de8.JPG)

1. Accept the default Credential Name and Role (Writer).  Select *Create New Service ID...* and provide a unique Service ID Name and Description. **DO NOT CLICK ADD**.

   ![Select Create New Service ID](https://user-images.githubusercontent.com/8126772/40882057-2a0bae26-66a5-11e8-870e-c6f569cfc676.JPG)

1. Scroll down and enter the following Configuration Parameter: `{"HMAC":true}`.  This tells the Service that you want to use a Hash-based Message Authentication Code) to access the Service. Click *Add*.

   ![Enter HMAC option and Click Add](https://user-images.githubusercontent.com/8126772/40882110-4b3b382c-66a6-11e8-8f73-5748d2e3bc60.JPG)

1. Click *View Credentials* and *Copy to Clipboard*.

   ![View and Save Credentials](https://user-images.githubusercontent.com/8126772/40882189-42c73108-66a8-11e8-8856-02bfcde402fc.JPG)

1. Save credentials to a text file for later use.

   ![Save Credentials to a text file](https://user-images.githubusercontent.com/8126772/40933201-ca58a302-67fe-11e8-91cb-cd507c8c0316.JPG)

## <a name="create_bucket">5. Create a Bucket</a>

1. Click *Buckets*; Click *Create bucket*; Provide a unique bucket name; Click *Create*.

   ![Create a bucket](https://user-images.githubusercontent.com/8126772/40936065-106fe91e-6808-11e8-9a5d-b14d56be9487.JPG)
