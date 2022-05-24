# Azure-Front-Door

# What is the purpose of Azure Front Door?
- It is a routing service that helps accerlate your application performance by routing traffic based on performance of your endpoints
- It works at layer 7 or HTTP/HTTPS
- This service will route client requests to the fastest and most available application backend


Features of Azure Front Door
- URL-based routing - here you can route traffic to your backend servers based on the URL paths of the request
- Multiple-site hosting - here you can configure more than one web site on the same front door configuration
- Session affinity - here you can keep a user session attached to the same application backend
- SSL terminations - SSL connections can be terminated at the Front Door itself 
- Web application firewall - protects web applications from internet-based attacks



# Use Case: Use Front Door to route traffic to one main web app and if the main web app is unavailable, redirect the traffic to the second wep app
- Deploy two Azure Web Apps 
- Deploy Azure Front Door
- Add the two backend pools for the web applications created


- When users hit the front door, we want clients to go to the primary web app
- To do that, ensure priority and weight is set. 
- Priority must be less than secondary web app


# Azure Front Door rules
- Rule just tells Azure Front Door how to route traffic to the backend pools


# Testing
- Access the primary web 
- Turn off the primary web server
- Access the primary web again and see where you will be directed to
- Azure Front Door has detected than the primary web app server is down, so it will redirect users to the secondary web app

# Difference between Azure Front Door and Azure Application Gateway
- Both have commmon features so why use it?
- Azure Front door is a <em> global service </em>
- Application gateways must have a region. It is a region-based resource.
- Ex: If admins deploy a application gateway in East US 2 region and it goes down, then the Applicationg gateway is down.


# Azure Front Door is global and highly available
- It can route traffic faster
- Also priority feature is available and not in Application gateway
