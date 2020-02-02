# Amazon-AWS-WAF-
 Web Application Firewall
Amazon AWS Confiuguring WAF to Block IP address
AWS WAF is a web application firewall service that helps protect your web apps from common exploits that could affect app availability, compromise security, or consume excessive resources

 

In here we have two instances called LinuxWebserver1 and Linux Webserver3 that are part of Application Load Balancer; and the goal is that my Ip address ( my laptop Ip address) will not be able to access this Website

 

Step 1) First I show you what I have with two instances

Step 2) When I go to Load Balancer on the left side and copy and paste long DNS name ; I will be able to see both content of the Websites (after refresh) that shows the ALB is working good.

Step 3) Or since I have “A” record on Route 53 , I can use the domain name on Route 53 , so life is good

 

Step 4) now goal is to block hamed2019.com so that my home PC Ip address will not be able to see it.

 

Step 5) go to WAF , click configure WEB ACL , on the Concepts overview , we will see what we can do it; so click next , then called it WebDenyACL

Syep 6) Pick the Region N.Va and then pick resources which  is Application Load Balancer , then click next

Step 7) now we will create a condition, as we see in video we can pick any of the condition

Cross-site scripting match conditions
Geo match conditions
IP match conditions
Size constraint conditions
SQL injection match conditions
String and regex match conditions
Step 8) Click create IP match condition

Step 9) Give the name “MyHomePC” then go to google and search what is my IP address ; and you will get the Ip address for example :

100.15.97.150

 

Step 10) put the above number 100.15.97.150/32 ( /24 means block and range of IP address ) /32means only that particular Ip address , then make sure click add Ip address

 

Step 11 ) Now we click next and then we want to create a Rule , on next page click Rule and called “HomePCRule”

Step 12) Then go to section “Add Condition” and do as follow”

When a Request “does” originate from an Ip address

                                           “MyHomePC” Then you will see IP address=100.15.97.32

 Then click create.

 

Step 12) On next page leave it as block then for default action, pick first one

               “Allow all request that does not match any rule”

 

Step 13) Click Review and create , that will take to next page ; then read it and click confirm and create

                                                

 

Step 14) Now go to left side and click on WebACL rule ; then click on “WebDenyACL” then go to tab called Rules ; then you should see all information.

Step 15 ) Now try to access the website ; by either copy and paste long DNS name from load balancer to use your domain name . you should see Forbidden Error 403

 

Step 16) Hint : when you click on “Web ACL” on left  ; then you might see few name on it ; when you click one of them ; then go to TAB Rules ; and then at bottom you will see add association . then you will see this :

 

You can associate only one web ACL with a specific resource. If a different web ACL is already associated with the selected resource, the association will be updated with this web ACL
