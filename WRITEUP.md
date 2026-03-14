# Project Overview

This project is aimed at showing the deployment of a Python-based Article Content Management System (CMS) on the cloud using Microsoft Azure. The objective of this project was to create a web application that utilizes various services offered by Microsoft Azure, including web hosting, SQL database storage, blob storage for images, and authentication through Microsoft identities.

The application allows users to create articles that contain information such as a title, author name, body of content, and an image. The images used in the articles are stored in **Azure Blob Storage**, whereas the articles are stored in an **Azure SQL Database**. The application also includes a logging feature and authentication for better security.

To deploy this application on Microsoft Azure, two major approaches could be employed: deploying the application on a Virtual Machine (VM) or deploying it through Azure App Service (Web App). In this case, I chose the second option: **deploying through Azure App Service (Web App)**.

---

## Reason for Choosing Azure App Service (Web App)

I decided to go with Azure App Service instead of deploying it on a Virtual Machine because it is a more efficient, scalable, and manageable way of hosting web applications. This is because it reduces the complexities of server management, allowing developers to focus on application development instead of server management.

The first reason why I chose to go with Azure App Service is that it is a **PaaS service** offered by Microsoft Azure. This is important because it means that the application is automatically provided with a server, operating system, and other services required for its operation, without having to manage them directly, unlike when deploying on a Virtual Machine.

The second reason why I chose to go with Azure App Service is that it **integrates very well with GitHub** for CI/CD pipeline deployment. This is important because it means that once a repository is created on GitHub, it can be easily connected to Azure App Service through its Deployment Center, allowing it to automatically build and deploy when changes are pushed to the repository.

Azure App Service also offers features like **application logging, monitoring, and configuration settings** for the environment. These are all important for debugging an application while it is deployed. The features enable better tracking of user activities, login attempts, etc.

Finally, Azure App Service offers a **free pricing tier called F1**, which is appropriate for a development environment. This is an advantage for the project since it can be deployed for free.

---

## Comparison of Deployment Options: VM vs. Azure App Service

For the Article CMS deployment, I analyzed two primary hosting strategies based on four critical metrics:

### 1. Cost Analysis
* **Virtual Machine (VM):** Higher operational cost. You pay for the allocated resources (CPU/RAM) regardless of actual traffic. Additional costs apply for managed disks and data redundancy.
* **Azure App Service:** More cost-efficient. It offers a Free (F1) tier for development and allows for granular scaling so you only pay for the capacity your application actually uses.

### 2. Scalability Analysis
* **Virtual Machine (VM):** Scalability is a manual process. Increasing capacity requires manual hardware upgrades or the complex configuration of Virtual Machine Scale Sets.
* **Azure App Service:** Supports automated horizontal and vertical scaling. The platform can automatically add instances or increase power based on real-time HTTP traffic or CPU load.

### 3. Availability Analysis
* **Virtual Machine (VM):** High availability must be configured and managed by the user. You are responsible for OS-level uptime, patching, and failover configurations.
* **Azure App Service:** Provides built-in high availability. Microsoft manages the underlying infrastructure and provides a guaranteed Service Level Agreement (SLA) for the platform uptime.

### 4. Workflow Analysis
* **Virtual Machine (VM):** Highly complex workflow. Requires manual setup of the OS, security patches, and web servers like Nginx or Apache to host the Flask app.
* **Azure App Service:** Extremely streamlined workflow. It features native integration with GitHub Actions for CI/CD, allowing for automated deployments without managing the underlying server.

### **Justification for Choosing Azure App Service:**
I chose Azure App Service because its PaaS (Platform as a Service) model allows me to deploy a secure, highly available application without the burden of server maintenance. This choice ensures that the application is always running on a patched, optimized environment, significantly reducing the risk of security vulnerabilities at the OS level.

---

## Architecture of the Application

The deployed application utilizes several Azure services that offer the complete functionality for the application. All resources for this project are contained within a **single, unified Resource Group** for organized management.

The **Azure App Service** hosts the Python Flask web application and delivers the CMS interface to end users. The app service hosts the app runtime environment and processes HTTP requests from users. 

The **Azure SQL Database** stores structured data for articles such as article title, author name, article body, and other data. SQL scripts from the repository were executed to create the required database tables for the application. 

The **Azure Storage Account** hosts uploaded images for articles via Blob Storage. When a user uploads an image while creating an article, the image is uploaded to a blob container. The application retrieves the uploaded images from the blob container endpoint. 

The application utilizes Microsoft authentication via **Microsoft Entra ID** for authentication. The application allows users to sign in using their Microsoft accounts via OAuth2 authentication. The redirect URIs for authentication are set in the app registration. 

The application has a **logging mechanism** that records both failed and successful login attempts. The log records can be viewed via the Azure App Service Log Stream. The log records help administrators identify potential security issues.

---

## Impact of Infrastructure Choice and Application Requirements

Choosing Azure App Service simplifies the application deployment by providing a pre-configured runtime, but it limits direct access to the underlying Operating System. If I had chosen a Virtual Machine, I would have had full control over the infrastructure, but it would have required me to manually install and configure a web server like Nginx or Apache to proxy requests to my Python application.

Because I chose a managed service, my application requirements shifted toward using external managed services for persistence. All article data is stored in **Azure SQL Database** and images are stored in **Azure Blob Storage** within a single, unified Resource Group. Additionally, I configured the application's logging strategy using `app.logger` to ensure that both successful and failed login attempts are captured directly by the Azure Log Stream, which is essential for monitoring in a managed PaaS environment.

---

## Deployment Process

The deployment process involved a series of steps for a successful deployment of the application on Azure.

1.  **GitHub Upload:** The first step was uploading the project repository containing the starter files and the application code onto **GitHub**. This repository contained all the necessary components for the application, including the application code, SQL scripts, and workflow files for deployment.
2.  **App Service Creation:** The second step was creating a new Azure App Service instance using the Python 3.10 environment. Then, the Deployment Center in Azure was connected to the repository on GitHub for automated build and deployment using GitHub Actions.
3.  **Environment Configuration:** The third step was configuring environment variables for the application on Azure App Service. This includes variables like database credentials, storage account details, and authentication secrets for the application. This is done by setting environment variables on Azure App Service.

The application was deployed successfully using the CI/CD pipeline, allowing the CMS web interface to be accessed via the Azure Web App URL.

---

## Application Features

The features that are being provided by the deployed application developed using the CMS are as follows:

* Creating articles with title, author, body, and image.
* Storage of articles in Azure SQL Database.
* Storage of images uploaded by users in Azure Blob Storage.
* Implementation of user authentication using Microsoft login integration.
* Logging of both successful and failed login attempts for the application.
* Continuous deployment using integration with GitHub.

This shows how various cloud computing services can be used together to create a cloud-based web application.

---

## Conclusion

In conclusion, Azure App Service was chosen as the platform for this project based on its ability to simplify hosting of web applications, including its powerful capabilities for deploying applications, monitoring, and scalability. This is compared to using a Virtual Machine, where operational complexities are eliminated, allowing developers to focus on development.

The integration of Azure App Service, Azure SQL Database, Azure Blob Storage, and Microsoft authentication makes this project a complete example of a cloud architecture that can be used for deploying a web application. The integration of automated deployments through GitHub is also an example of modern DevOps principles and effective cloud application management.

This project is therefore a success in demonstrating how Azure services can be integrated for deploying a secure, scalable, and fully functional web application in the cloud environment.