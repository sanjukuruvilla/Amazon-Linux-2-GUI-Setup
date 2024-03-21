## Table of Contents

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Tasks](#tasks)
    - [Creating IAM Resources](#creating-iam-resources)
    - [Configuring AWS CLI](#configuring-aws-cli)
    - [Setting Up Amazon Linux 2 EC2 Instance](#setting-up-amazon-linux-2-ec2-instance)
    - [GUI Desktop](#gui-desktop)
4. [Additional Documentation](#additional-documentation)
5. [Contributing](#contributing)
6. [License](#license)

# Amazon-Linux-2-GUI-Setup

## Overview

This guide provides step-by-step instructions on how to enable the GUI interface on an Amazon Linux 2 EC2 instance using AWS CLI commands. By following these instructions, you'll be able to create necessary resources, configure permissions, and set up the GUI environment for remote access.

## Prerequisites

Before you begin, ensure you have:

- An AWS account with appropriate permissions to create and manage IAM resources.
- AWS CLI installed and configured on your local machine.

## Tasks

### Creating IAM Resources

1. **Create a Group**: 

```bash
aws iam create-group --group-name [Group Name]
```

2. **Attach Policies to the Group**: 

```bash
aws iam attach-group-policy --group-name [Group Name] --policy-arn [Policy ARN]
```
*(Repeat the above process for each policy)*

3. **Create a User and Add to the Group**:

```bash
aws iam create-user --username [Username]
aws iam add-user-to-group --user-name [Username] --group-name [Group Name]
```

4. **Give the User a Password**:

```bash
aws iam create-login-profile --user-name [Username] --password [Password]
```
*(Optional: Create Access Keys)*:

```bash
aws iam create-access-key --user-name [Username]
```

### Configuring AWS CLI

1. **Configure AWS CLI with User Credentials**:

```bash
aws configure
```

2. **Enter Your Access Key ID and Secret Access Key**.

### Setting Up Amazon Linux 2 EC2 Instance

1. **Launch EC2 Instance**:

```bash
aws ec2 run-instances --image-id [Image ID] --instance-type [Instance Type] --key-name [Key Name] --subnet-id [Subnet ID] --security-group-ids [Security Group ID] --associate-public-ip-address --region [Region]
```

2. **Update the Kernel**:

```bash
yum clean all -y
yum update -y
yum upgrade -y
```

3. **Install Desktop GUI Environment**:

```bash
yum groupinstall "Mate-desktop-environment"
```

4. **Create a User with Administrative Privileges**:

```bash
useradd -m -s /bin/bash [Username]
passwd [Username]
usermod -aG wheel [Username]
```

5. **Change Default Booting Process to GUI**:

```bash
systemctl set-default graphical.target
systemctl reboot
```

6. **Connect to Linux via RDP Tool**:

- Open RDP tool and connect using public IP, username, and password.

### GUI Desktop

After successful configuration and setup, you'll be able to access the GUI desktop of your Amazon Linux 2 EC2 instance remotely.

## License

This project is licensed under the [MIT License](LICENSE).
