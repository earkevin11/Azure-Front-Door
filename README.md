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

# Create one two web apps using Azure Web App service and create an html page using App Service Editor

- Configure primaryapp1 web app in Central Region

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170124897-5eb73dd0-b451-4512-8735-42d6644fe248.png" height="90%" width="90%" alt="front door"/>

<p/>

- Configure primaryapp1 web app in East Region

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170124921-4a5e09ae-8bed-4210-bf61-aa3917e0efd5.png" height="90%" width="90%" alt="front door"/>

<p/>

- Use app service editor

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170124643-462bde17-3a50-4b5d-ac4c-cfc2ca11f2c6.png" height="90%" width="90%" alt="front door"/>

<p/>

- This is what users will use to acccess primary web app 

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170126057-f951662b-5375-4791-b07c-acd1035ee6aa.png" height="90%" width="90%" alt="front door"/>

<p/>

- This is the <em> primarywebapp1 web page </em>

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170126502-f6091c05-9ff8-4cd3-8353-645208edfe7b.png" height="90%" width="90%" alt="front door"/>

<p/>

- This is what users will use to access the secondary web app
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170126774-aec1eac8-f72c-49ce-aca6-a0c2ec63fbbe.png" height="90%" width="90%" alt="front door"/>

<p/>


- Result of the secondary web app

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170126599-9d77bfb7-d193-41b0-a680-6a6dc0d664e9.png" height="90%" width="90%" alt="front door"/>

<p/>
                                                                                                                                                
                                                                                                                                                
# Create Azure Front Door
- Add a host name - this is what users wil use to access your web apps

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170130359-a1bfe960-5048-4e56-8025-4e308fed848e.png" height="90%" width="90%" alt="front door"/>

<p/>

# Add a backend pool
- This is where your web apps will be stored
- Priority is 1 because we want the Azure Front Door to direct traffic to this primary web app
                                                                                                                                           
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170131418-e19db17a-897e-4207-a570-28d120643ad8.png" height="90%" width="90%" alt="front door"/>

<p/>

# Secondary web app
- Notice that we made priority 2 because we want users to access the primary web app first
- Secondary web app will only be accessed if the primary web app is down or out of service

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170131469-53f6ceab-72c8-44aa-b667-4524145cf8f6.png" height="90%" width="90%" alt="front door"/>

<p/>

- Leave all settings as is and add the backend pool

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170131855-69b32d78-d894-406e-bc4b-23231ecb7bd5.png" height="45%" width="45%" alt="front door"/>

<p/>

- When users hit the Azure Front door domain - kevinfrontdoorservice.azurefd.net , it will route to the backend pool (kevinbackendpool) that was created
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170132129-301e25ac-4dfb-4ee5-a7dc-44a8f1684a8f.png" height="45%" width="45%" alt="front door"/>

<p/>





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

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170132129-301e25ac-4dfb-4ee5-a7dc-44a8f1684a8f.png" height="45%" width="45%" alt="front door"/>

<p/>

- Access the frontdoor created using https://kevinfrontdoorservice.azurefd.net

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170132765-ffc1a793-ace7-45ac-b544-d02d3f1668d5.png" height="150%" width="150%" alt="front door"/>

<p/>

- This is the result of Azure Front Door
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170133117-80182d9b-bdf7-4d43-ae93-b64b601cd222.png" height="150%" width="150%" alt="front door"/>

<p/>

- Turned off the primary web app and refresh
- See that it led to the secondary web app and that is all because of Azure Front Door
- Admins may have to wait a couple of minutes for Azure Front Door to redirect the request to the secondary web app

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170133917-fe9a132b-d333-46a2-8648-70ba0a6c7d46.png" height="150%" width="150%" alt="front door"/>

<p/>



# Difference between Azure Front Door and Azure Application Gateway
- Both have commmon features so why use it?
- Azure Front door is a <em> global service </em>
- When creating Azure Front Door, no region is requested.
- Application gateways must have a region. It is a region-based resource.
- Ex: If admins deploy a application gateway in East US 2 region and it goes down, then the Applicationg gateway is down.


# Azure Front Door is global and highly available
- It can route traffic faster
- Also priority feature is available and not in Application gateway
