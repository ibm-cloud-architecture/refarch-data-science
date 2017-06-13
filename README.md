# Create an analytics application in IBM Data Science Experience (DSX) and Deploy it in Watson Machine Learning (WML) 

## Table of Contents

- [Create an analytics application in IBM Data Science Experience (DSX) and Deploy it in Watson Machine Learning (WML)](#)
	- [Introduction](#introduction)
	- [Services used in the reference architecture](#services-used-in-the-reference-architecture)
	- [Application and Use Case Overview](#application-and-use-case-overview)
	- [Project files](#project-files)
	- [Run the reference application in IBM Cloud](#run-the-reference-application-in-ibm-cloud)
		- [Step 1: Environment Setup](#)
			- [Prerequisites](#)
		- [Step 2: Review the notebook, deploy and test model in WML](#)
		- [Step 3: Test deployed service with a Python Flask application](#)
		- [Step 4 (optional): Connect project to a new Bluemix Spark Service](#)
		- [Step 5 (optional): Access data in dashDB Bluemix service](#)

## Introduction
This project provides a reference implementation for creating analytics deployment architecture with Data Science Expeience (DSX) and Watson Machine Learning (WML). Optional components of the architecture are Bluemix dashDB (data source), Bluemix Apache Spark (additional runtime environment), and Python Flask (front end) services. dashDB service is optional because other data sources can be used. Additional Spark service is optional because DSX already includes Spark. Python Flask is optional because other types of front end applications can integrate with analytics.
 
The logical architecture for this reference implementation is shown in the picture below.

![Architecture](static/imgs/architecture.PNG?raw=true)

In this tutorial you will complete the following steps
1. Review predictive model implementation (Python Notebook) in DSX. 
2. Deploy SparkML model for on-line scoring in WML.
3. Test the model with a Python Flask application. 

Optional steps are:
1. Create a Spark service in Bluemix and connect it to the DSX project. 
2. Modify the notebook to connect to a dahsDB data source. 

## Services used in the reference architecture
The reference architecture uses the following IBM services and offerings.

**Data Science Experience**
DSX is a comprehensive platform for developing analytics applications. The main development environment is Notebooks, which supports development in Python, R, and Scala. DSX also includes R Studio - software by an IBM business partner which has been integrated in DSX, and APIs for developing **Decision Optimization** applications. DSX environment connects to a Spark service, which provides highly scalable environment for running analytics. 

**Watson Machine Learning**
WML service includes three types of capabilities: 
a. Online, batch, and streaming deployment of SparkML and Python scikit-learn models
b. Repository for models
c. Wizards for simplifying creation of SparkML models
WML is integrated in the DSX UI, and it's also accessible through APIs (Python, R, Scala) and via UI in the Bluemix WML service. 

**Spark Service**
Spark Service is included with DSX by default. If a user wants more processing power, they can connect DSX/WML projects to a Spark Service configured in Bluemix. 

**dashDB Bluemix Service**
DSX can connect to Bluemix dashDB service, as well as many other types of cloud and on-premise data sources. DSX includes "Connector API" for over 20 data sources. Connector API simplifies and streamlines access to different types of data sources. If a data source is not supported by the Connector API, the standard data source connection approach (for example, a jdbc driver) can be used. Please note that Secure Gateway Bluemix service is required for accessing on-premise data sources. 

**Python Flask Bluemix Service**
After models are deployed in WML they can be accessed via REST APIs. We created a sample client application in Python Flask, a popular Web programming API. Any on-premise or cloud application that can integrate with a REST API can invoke models deployed in WML. 

## Application and Use Case Overview
Our example implements a predictive model for telco churn. We chose telco churn as an example because it's easy to understand, and at the same time it implements frequently used analytics approach - a classification model to predict churn. The notebook that implements the use case provides more details about the use case and analytics implementation. 
 
## Project files
This project contains all the required files for building out the architecture and completing the tutorial.
1. Notebooks
2. Data
3. Python Flask application

## Run the reference application in IBM Cloud
To run the sample applications you will to complete several steps in DSX, WML, and optionally, in dashDB, Spark, and Python Flask services.  

### Step 1: Environment Setup

#### Prerequisites

1. Download this repository to your laptop and unzip it.
2. Sign up for [DSX](https://datascience.ibm.com/) and [Bluemix](https://bluemix.net). Make sure to use the same userid (otherwise Bluemix services will not be available in DSX)
3. In Bluemix, provision the following services
- [Watson Machine Learning](https://console.ng.bluemix.net/catalog/services/ibm-watson-machine-learning/?env_id=ibm:yp:us-south)
- [dashDB for Analytics](https://console.ng.bluemix.net/catalog/services/dashdb-for-analytics?env_id=ibm:yp:us-south&taxonomyNavigation=apps)
- [Spark](https://console.ng.bluemix.net/catalog/services/apache-spark?env_id=ibm:yp:us-south&taxonomyNavigation=apps)
- [Python Flask](https://console.ng.bluemix.net/catalog/starters/python-flask?env_id=ibm:yp:us-south&taxonomyNavigation=apps)

### Step 2: Review the notebook, deploy and test model in WML
1. Log in to [DSX](https://datascience.ibm.com/)
2. Click on the "+" icon to create a new project with a name *Data Science Use Case* **Note: it's important to use this name because the sample Notebook references it)**
![New Project](static/imgs/NewProject.PNG?raw=true)
3. Switch to the **Settings** tab and add two services - Watson Machine Learning and Spark. Select *Existing Services* (because they were created during the prerequisite step in Bluemix)
![Associated Services](static/imgs/AddServices.PNG?raw=true)
3. Switch to the **Data Assets** tab and load the data files - *churn.csv* and *customer.csv* (located in the /data folder). If the Files menu is not displayed, click on the Data icon ![Data icon](static/imgs/DataIcon.PNG?raw=true)
![Loaded Files](static/imgs/LoadedFiles.PNG?raw=true)
4. Use the "+" icon to create the Notebook from file. Browse to *TecloChurn.ipynb* file included with this project. 
5. Click on the Edit (pencil) icon to enter the edit mode. The notebook is in the edit mode when you see the menu. Follow instructions in the notebook.
![Notebook in the edit mode](static/imgs/NotebookEditMode.PNG?raw=true)

### Step 3 (optional): Test deployed service with a Python Flask application
The notebook provided instructions for testing the model with a REST client. We also developed a sample Python Flask application which can be used for testing: https://churndemo.mybluemix.net/. This application implements the REST client call to the model. 

### Step 4 (optional): Connect project to a new Bluemix Spark Service
As mentioned earlier, a DSX account (enterprise and free) by default includes a Spark Service. If you would like to add additional processing capacity, you can create a Spark Service in Bluemix and use it in your DSX projects. 

If you haven't already added a Spark Service from Bluemix to your project, add it in the **Additional Services** tab in the DSX project - see (3) **in Step 2**.  

Now when you create a new notebook, you can select which Spark Service you would like to use.
![Select Spark Service](static/imgs/SelectSparkService.PNG?raw=true)

### Step 5 (optional): Access data in dashDB Bluemix service
1. Log in to Bluemix and open the dashboard of your dashDB service. Note *Service credentials* information (paste into Notepad). 
2. Load *churn.csv* and *customer.csv* files. Select *Load into new table* and accept all defaults.
3. Log in to DSX and open *Data Science Experience* project.
4. In DSX, create a new notebook titled **TelcoChurn_dashDB** from file *TelcoChurn_dashDB.ipnb* (located in the *notebooks* folder) and follow instructions in the notebook. 

You have finished implementing the Data Science Use Case reference architecture in IBM Cloud. 
