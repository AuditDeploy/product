# Deployment Overview/Technical Requirements
Other than what you currently have running in your environment, Capture will be one single instance that will help you see your data. 

### Technical Requirements of Capture
Minimum | Recommended
 --- | --- 
Minimum CPU: 2		| Recommended: 4
Minimum ram: 12		| Recommended: 16

Required OS: Ubuntu 18.04 lts

Minimum Storage: 40Gb	

# Install Steps

1. Launch your instance of Capture (Make sure that you have more than 12 gb of Ram on the instance), make sure that you have enabled http
 and https access for the instance on launch. Ports: 80 and 443.
2. Once the Capture instance has fully launched(5 minutes), you should be able to access the UI to input your information that will give
 you access to the rest of Capture.
3. Once inside the Capture UI, you’ll have the option to look at logs(which will be empty on a fresh instance), users, and the shippers.
 Navigate to the shippers.
4. At the shippers tab, click the Configure button to set up your shipper
Specify a Name and port that you will have available on the instance you will install the shipper to(this will ship the logs that you 
specify from a machine in your environment to capture’s) then specify the type of module, Log Type(such as apache or nginx), path to the 
log file if you’re tailing a log file or port for a hook module, add any tags you want associated with these logs and add the module. Now 
you can submit this configuration and should see it appear in the UI. It will say “shipper awaiting start”. 

6. Once you’ve added the module you can either download the shipper binary from the ui (in the /Shippers/Manage route) and then scp it 
into your machine, or you can use the wget command shown on the ui in the download modal.
7. ssh onto the machine where you are installing the shipper.
8. mkdir log-shipper and cd into this directory (optional)
9. Run your wget or scp the zip onto this machine (in the log-shipper directory)
10. Unzip or tar xf the downloaded file.
11. If you run ls  you should now see capture-config.json and log-shipper-[operating system] (Ex: log-shipper-linux) in your current directory.
12. Now copy the shipper-id from the UI that you configured in step 5. 
13. On the machine with log shipper binary run 

sudo ./log-shipper-linux -i [shipper id]

14. The shipper will now begin sending logs from whichever files it’s been configured to track or send records via a webhook if this is how you’ve configured it.
15. Back on the Capture UI you should be able to refresh and see that the shipper has a green border across the top. This indicated the
 installation was successful and that the shipper is healthy. 

If you'd like to run the shipper as a continuously running service file, an example of that is below
```
[Unit]
Description=capture log shipper - starts shipperservice-service
After=network.target
[Service]
WorkingDirectory=/opt/log-shipper
Type=simple
User=root
ExecStart=/opt/log-shipper/log-shipper-linux
StandardOutput=file:/var/log/cshipper.log
StandardError=file:/var/log/cshipper.log
Restart=on-failure
[Install]
WantedBy=multi-user.target
```