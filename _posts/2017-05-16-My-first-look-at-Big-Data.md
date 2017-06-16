---
layout: post
title:  "First look at Big Data"
---

My notes on the first look at AWS(EC2, S3), Hadoop and Spark (getting through the installations and login)

### AWS
- EC2 Elastoc Cloud Computing
    Instance - Virtual Machine
    AMI - Snapshot of our Machine ot boot an instance(VM). It is possible to save a running instance to an new AMI...
    SSH - Key pair to connect to an instance(VM) remotely.

    `https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/`

    Lanuch your instance
- S3 Simple Storage Service
    Buckets - Unique Containers to stoe your files
    `https://aws.amazon.com/getting-started/tutorials/backup-files-to-amazon-s3/`

    `https://github.com/aws/aws-cli`
    `pip install awscli`

    `https://aws.amazon.com/getting-started/tutorials/backup-to-s3-cli/`

    Create aws bucket from command line
    delete add files from command line
    https://github.com/toddm92/aws/wiki/AWS-CLI-Cheat-Sheet

    Run EC2 from Command line

### Hadoop

- Introduction to MapReduce Algorithm

What is Hadoop?
- A very common implementation of the map-reduce framework

My first time around Big data and Hadoop!
1. Install Virtual box

- Install Virtualbox
    A simulated computer running on a host computer (our laptops).

2. Install Vagrant in root folder
    - vagrant init hashicorp/precise64
        A `Vagrantfile` has been placed in this directory. You are now
        ready to `vagrant up` your first virtual environment! Please read
        the comments in the Vagrantfile as well as documentation on
        `vagrantup.com` for more information on using Vagrant.

    - vagrant up
        Bringing machine 'default' up with 'virtualbox' provider...
    
    - vagrant destroy

3. Setup Vagrant Project   
    $ mkdir vagrant_getting_started
    $ cd vagrant_getting_started
    $ vagrant init
    // Copy the virtualbox and the vagrant file fromt he dropbox to the location. then from that location:
    vagrant up
    // smome configurations are loaded
    Then check the Virtual box UI - ur big data virtual machine will be running there. Press Start green button from there. when u are prompted for login go back to command line and Press
    vagrant ssh
    //give password if asked. Then get bigdata
    bigdata_start.sh 
    // Connect to resource management platform using YARN from your browser
    http://10.211.55.101:8088/cluster
    // Now when u type exercise 2 and 3
    // results are seen int he hadoop broqser window
    

### Spark
    It is machine learning like Scikit learn 
    Installation - go through 9.2.2 spark installation guide
    