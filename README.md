# Using IBM Cloud Object Storage from a Command Line Interface
This tutorial provides an overview of setting up and using IBM COS from a Command Line Interface.
1. [Prerequisites (MAC with Python, IBM Cloud account, etc)](#pre-reqs)
1. [Download and install the AWS CLI package](#dwnl_awscli)
1. [Create an instance of the IBM COS Service](#create_cos)
1. Create and Save Service Credentials
1. Create a Bucket
1. Upload Files to the bucket
1. Configure the AWS CLI with IBM COS credentials
1. Create LM (lazy man) script
1. Run scenarios (prefixes, cp, sync, static web hosting, presigned URIs, getting files on S3, etc.)


## <a name="pre-reqs">1. Prerequisites</a>
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

## <a name="create_cos">Create an instance of the IBM COS Service</a>

1. Login into the IBM Cloud console, navigate to the Catalog, search for Object Storage, and click on it.

   ![Login to IBM Cloud, navigate to the Catalog, search for Object Storage, select plan](https://user-images.githubusercontent.com/8126772/40881643-f1b6f1d0-6699-11e8-9060-a26cf088689b.JPG)

1. The *Lite* plan is automatically selected for you. Click **Create**.

   ![Click Create](https://user-images.githubusercontent.com/8126772/40881642-f1ac77d2-6699-11e8-958c-95321866afae.JPG)
