# Deployment Overview/Technical Requirements
Other than what you currently have running in your environment, Capture will be one single instance that will help you see your data. 

### Technical Spec. Requirements of Capture
Minimum | Recommended
 --- | --- 
Minimum CPU: 2		| Recommended: 4
Minimum ram: 12		| Recommended: 16

Required OS: Ubuntu 18.04 lts

Minimum Storage: 40Gb	

### Deployment Steps
1. Once the image/ami is in your tenancy, launch an instance with either the Minimum or Recommended Spec requirements
2. Make sure to have http/https enabled on the instance, recommended wait time after launching is 5 minutes

### Skills Needed
General Understanding of how to launch an instance from image/ami within your cloud provider

### SSH needs
If you need to restart the service, you can use ssh keys within your tenancy then ssh as a super user
Once inside, you only need to run the command
```
sudo systemctl restart capture-service.service
```

### Other Requirements
An account with the cloud provider (AWS, Azure, GCP, or Oracle)

The appliance does not require root access, Capture will spin up on launch from image/ami.


### Deployment Best Practices
[AWS Best Practices IAM][https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html]

[Azure Deployment Best Practices][https://docs.microsoft.com/en-us/azure/app-service/deploy-best-practices]

[GCP Best Practices Cloud Security][https://cloud.google.com/security/best-practices]

[Oracle Best Practices Cloud Infrastructure][https://www.oracle.com/technetwork/articles/systems-hardware-architecture/o11-050-cloud-iaas-vm-405449.pdf]