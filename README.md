Tools and code used during my talk at RootedCON 2017
========

[__Automate or Die! How to survive to an attack in the cloud__](http://rootedcon.com)

March 3rd, 2017

------
##CloudFormation Template
Template used for demos is based on my existing CFN template to automate deploy of Security Monkey. For additional steps after deployment please go to that repo documentation here [here](https://github.com/toniblyx/security_monkey_cloudformation)
###What does this CFN template?
1. Creates a VPC with a public subnet for two instances and a private subnet for RDS (Pgsql used by SecurityMonkey)
2. One instance is dedicated to Security Monkey the other has Tools and sample code on it like: [Prowler](https://github.com/Alfresco/aws-cis-security-benchmark), [ThreatResponse Tools](https://github.com/ThreatResponse) (see the template for details)

##Presentation in PPTX format
See file __Automate or die - Rootedcon 2017.pptx__ in this repo. You can easily use all links in the __References__ slide. All links below in this README. That presentation contains also hidden slides that I didn't show during my talk. 

##Some commands used during my Demo
1- Instance Role - metadata server:

* ```curl http://169.254.169.254/latest/meta-data/iam/security-credentials/```
* ```curl http://169.254.169.254/latest/meta-data/iam/security-credentials/SampleRole-17TS7M8I11W2K```
* ```aws sts get-session-token --duration-seconds 129600```
* ```aws ec2 describe-instances```
* ```aws ec2 create-key-pair --key-name admin666 --output text```


2- Mad-King attack (Tools Instance): 
[Demo Video mad-king](https://www.youtube.com/watch?v=9Jp9nGhpS0w) 

* ```cd /opt/mad-king```
* ```aws configure``` use valid keys 
* ```virtualenv .```
* ```source bin/activate```
* ```zappa deploy production``` and go to output URL

3- Incident Response aws_ir (Tools Instance): 

[Demo Video host compromise](https://www.youtube.com/watch?v=_UezvE0OGaA)

[Demo Video key compromise](https://www.youtube.com/watch?v=-OY0L4BMyLY)


* ```aws_ir key-compromise --access-key-id AKIAJTEST```
* ```aws_ir instance-compromise --instance-ip IP --user centos --ssh-key ~/key-toplay.pem --repository-url https://threatresponse-lime-modules.s3.amazonaws.com```
* ```volatility -f IP-2017-02-23T02\:15\:48-mem.lime imageinfo```
* ```volatility -f IP-2017-02-23T02\:15\:48-mem.lime --profile=Ubuntu14043 linux_pslist```

4- Hardening template, Prowler, SecurityMonkey 

[Demo Video](https://www.youtube.com/watch?v=xeAfXc9rIwU)

* hardening template from [here](https://github.com/awslabs/aws-security-benchmark/tree/master/aws_cis_foundation_framework)
* run prowler (ssh to Tools Instance, aws-cli must be configured)
* ```cd /opt/aws-cis-security-benchmark```
* ```./prowler```
* show securitymonkey


5- Cleanup demo!!

* Delete CFN Stacks, SSH keys and Access keys!

##All links and tools mentioned during the talk in order of appearance 

* Become an IAM Ninja: [https://youtu.be/Du478i9O_mc](https://youtu.be/Du478i9O_mc) 
* [http://threatresponse.cloud/ ](http://threatresponse.cloud/)
* [https://github.com/capitalone/cloud-custodian]()
* [https://github.com/awslabs/aws-security-benchmark/tree/master/aws_cis_foundation_framework]()
* [https://github.com/ThreatResponse/mad-king]() 
* [https://danielgrzelak.com/backdooring-an-aws-account-da007d36f8f9#.ut0x2bjv5]()
* [https://github.com/Miserlou/mackenzie]() 
* Gone in 60 Millisecons (33c3): [https://www.youtube.com/watch?v=YZ058hmLuv0]()
* [https://github.com/dagrz/aws_pwn ]()
* Serverless Security [https://www.rsaconference.com/writable/presentations/file_upload/asd-f01_serverless-security-are-you-ready-for-the-future.pdf]()
* [https://github.com/devsecops/lambhack]() 
* [https://blyx.com/2016/03/11/forensics-in-aws-an-introduction/]()
* [https://blyx.com/2016/06/16/cloud-forensics-caine7-on-aws/]()
* [https://s3-us-west-2.amazonaws.com/threatresponse-static/us-16-Krug-Hardening-AWS-Environments-and-Automating-Incident-Response-for-AWS-Compromises-wp.pdf]() 
* [https://aws.amazon.com/premiumsupport/trustedadvisor/]()
* [https://aws.amazon.com/cloudtrail/]()
* [https://azure.microsoft.com/en-us/resources/videos/azure-operational-insights-overview/]()
* [https://aws.amazon.com/cloudformation/]()
* [https://aws.amazon.com/config/]()
* [https://github.com/Alfresco/aws-cis-security-benchmark]() 
* [https://github.com/nccgroup/Scout2]()
* [https://github.com/Netflix/security_monkey]()
* [https://github.com/Netflix/edda]()
* [https://github.com/Netflix/Fido]()
* [https://github.com/capitalone/cloud-custodian]()
* [https://github.com/awslabs/aws-security-benchmark]()
* [https://github.com/cloudsploit]()
* [https://github.com/widdix/aws-cf-templates/tree/master/security#account-password-policy]()
* [https://github.com/jantman/awslimitchecker]()
* [https://blogs.msdn.microsoft.com/azuresecurity/2017/01/04/get-hands-on-experience-with-oms-security-with-oms-suite-experience-center/]()
* [https://github.com/spotify/gcp-audit]()
* [https://github.com/awslabs/git-secrets]()

