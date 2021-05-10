# Deploy a High Availability Web App

## Introduction

Your company is creating an Instagram clone called *Udagram*. Developers
pushed the latest version of their code in a zip file located in a public S3
Bucket.

### Problem

Deploy this application along with necessary supporting software into its
machine infrastructure.

This should be done in an automated fashion so that the infrastructure can
be discarded as soon as the testing team finishes their tests and gathers
their results.

## Work Flow

### Diagram

First develop a diagram to present as a visual aid to understand the
CloudFormation script.

### Script (Template and Parameters)

Develop a script to interpret the instructions and create a matching
CloudFormation script.

## Dependencies

### Server Specs

  1. Create a *Launch Configuration* for your application servers in 
order to deploy four servers, two located in each of your private 
subnets.

    * The launch configuration will be used by an auto-scaling group

  2. You'll need two vCPUs and at least 4GB of RAM
    
    * The OS to be used is `Ubuntu 18`
    * Choose an Instance size and Machine Image (AMI) that best fits 
this spec

  3. Allocate at least 10GB of disk space so that you don't run into 
issues

### Security Groups and Roles

  1. Since you'll need to download the application archieve from an S3 
bucket, you'll need to create an IAM role that allows your instance to 
use the S3 service

  2. *Udagram* communicates on the default `HTTP Port: 80`, so your 
servers will need this inbound port open since you'll use it with the 
Load Balancer and the Load Balancer Health Check

    * As for outbound, the servers will  need unrestricted internet 
access to be able to download and update their software

  3. The load balancer should allow all public traffic (`0.0.0.0/0`) on 
`port 80` inbound, which is the default `HTTP port`
  
    * Outbound will only be using `port 80` to reach the internal 
servers

  4. The application needs to be deployed into private subnets with a 
Load Balancer located in its public subnet

  5. One of the output exports of the CloudFormation script should be 
the public URL of the Load Balancer.

  6. (*Bonus*) Add `http://` in front of the load balancer's `DNS Name` 
in the output for convenience
