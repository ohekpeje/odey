## Configure Windows client with pGina.

pGina is a pluggable, open-source credential provider (and GINA) replacement. It allows for alternate methods of interactive user authentication and access management on machines running the Windows operating system.

Download and install pGina stable version setup from (https://github.com/pgina/pgina/releases/v3.1.8.0)
 
This configuration was performed within a virtual box.

To start check/verify the IP of your windows machine using ***ipconfig ***

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744603261/U1l__pEEZ.png)


After installation of pGina, launch pGina application.
 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744691321/01djjmRUQ.png)


Click on Plugin selection and check all 3 boxes as shown in the image below.
Plugin Name: LDAP: Authentication, Authorization and Gateway, then click on configure to continue the set-up.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744721945/CmrYzvO00.png)
 
Fill in the required information.

For LDAP host, we use the IP of or machine 10.0.2.15 which is advisable to use in case you make a mistake the hostname and users would be unable to access.

For the LDAP Port, we do not require to make any changes to the port.

Edit the Search DN and edit the required information and replace it with your own ldap server details dc=labwork,dc=local. Fill in the rest as shown and click on save.
 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744749670/Yzk5tT-09.png)

Click on Plugin Order, select the LDAP plugin and use the arrow provided to move it to the top.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744772888/4mSHSSf1a.png)
 

Click on the Simulation tab next as we would try to simulate using an actual user to check if our set-up I correct.

Here we use the user which is the name attached to your machine upon creation and the password of the machine.
 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744822423/3WU9nx94k.png)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744815446/blFtR-JIs.png)

Then you can click on apply and save & close. Shut down your machine and try logging in with the user as used in the simulation.
 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744837040/W3FOaJFV6.png)
 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643744850195/nR4f2Xhpx.png)
 
# Conclusion
You are now ready to use pGina to log into Windows machines!