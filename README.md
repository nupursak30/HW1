# HW1

### Pre-requisites
1. The CoffeMaker server already has permissions to access the private git repository required for the configuration of CoffeMaker server(done via ssh forwarding through the ansibleVM), so that cloning the private repository won't throw any exceptions.

### CoffeMaker Server
1. The ansible playbook for the CoffeMaker Server configuration:[coffemaker_playbook](coffemaker.yml)
2. During the screencast, CoffeMaker Server IP address was 192.168.33.60
3. Using Vagrant, we need to provision **2048** MB memory for the CoffeMaker server instead of provisioning it with the default value of "1024"
4. In order to test the ansible playbook, just go inside the ansibleVM and run the following command:  
  i. **ansible-playbook <coffemaker_playbook_location_path> -i inventory**  
  ii. The inventory file used for the playbook is : [inventory](inventory) wherein the host-group "coffemaker" is used for the coffemaker-server.  
  iii. Based on the host-group name assigned in the inventory file, the **hosts** section present in the [coffemaker_playbook](coffemaker.yml) script needs to be updated.  
  iv. User needs to input the root password which will be set for accessing the mysql server at the start of the [coffemaker_playbook](coffemaker.yml)  
  v. After the playbook is successfully exited, go to the web browser after sometime and type the following: 192.168.33.60:8080 (i.e. <Coffemaker_server_IP>:8080).This should open up the CoffeMaker HomePage. Go inside the Update Inventory section and check the value of the variables.By default, it will be 15.
  vi. As the mvn test is running in background so that the ansible playbook can exit, hence the playbook exits before maven command gets completed. Because of this reason, it may happen that the web server gets started after sometime(~3-4 min) when the mvn test is finally completed.  

### Selenium Server
1. The ansible playbook for the Selenium Server configuration:[selenium_playbook](selenium.yml).Make sure that the CoffeMaker server is already running before testing the Selenium playbook script.
2. During the screencast, Selenium Server IP address was 192.168.33.140
3. In order to test the ansible playbook, just go inside the ansibleVM and run the following command:  
  i. **ansible-playbook <selenium_playbook_location_path> -i inventory**  
  ii. The inventory file used for the playbook is : [inventory](inventory) wherein the host-group "selenium" is used for the selenium-server.  
  iii. Based on the host-group name assigned in the inventory file, the **hosts** section present in the [selenium_playbook](selenium.yml) script needs to be updated.  
  iv. User needs to input the IP address assigned to the **CoffeMaker** server at the start of the [selenium_playbook](selenium.yml).In my case, it was **192.168.33.60**  
  v. After the playbook is successfully exited, we will be able to see that the build is successful with no failures/errors indicating that the selenium testcases got passed. After this, go to the web browser and type the following: 192.168.33.60:8080 (i.e. <Coffemaker_server_IP>:8080).This should open up the CoffeMaker HomePage. Go inside the Update Inventory section and check the value of the variables(coffee,tea,etc.).The value of these variables should have been updated to a new value (new value=16 when both the playbooks are executed for the first time), indicating that the Selenium test cases were passed successfully.
  vi. Sometimes it might happen that an error is thrown when the [selenium_playbook](selenium.yml) is executed for the very first time. However, even in this case, if you go/refresh to the inventory section of the CoffeMaker homepage,you will see the value of those variables still got updated. In this case, just run the [selenium_playbook](selenium.yml) for second time and this time the build will be successful as well as the values will be updated  for those variables.  
  
### Screencast
Link: [Screencast_video](https://youtu.be/69XLAbjXQQU)
  
  
  
  
  

