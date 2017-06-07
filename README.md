# refarch-data-science

# Create an analytics application in IBM Data Science Experience (DSX) and Deploy it in Watson Machine Learning (DSX) 

## Table of Contents

## Introduction
This project provides a reference implementation for creating analytics deployment architecture with Data Science Expeience (DSX) and Watson Machine Learning (WML). Optional components of the architecture are Bluemix dashDB service (data source), Bluemix Apache Spark service (additional runtime environment), and Flask (front end) services. dashDB service is optional because other data sources can be used. Additional Spark Service is optional because DSX already includes Spark. Flask is optional because other types of front end applicaitons can integrate with analytics.
 
The logical architecture for this reference implementation is shown in the picture below.

**EL TODO**

![Application Architecture](static/imgs/app_architecture.png?raw=true)

In this tutorial you will complete the following steps
1. Review predictive model implementation (Python Notebook) in Data Science Experience. 
2. Deploy SparkML model for on-line scoring in Watson Machine Learning
3. Test the model with a Python Flask application

Optional steps are:
4. Create a Spark service in Bluemix and connect it to the DSX project
5. Modify the Notebook to connect to a dahsDB data source
6. Create a model with the Watson Machine Learning wizard

## Services used in the reference architecture
The reference architecture uses the following IBM services and offerings.

**Data Science Experience**
Data Science Experience (DSX) is a comprehensive platform for developing analytics applications. The main development environments are Notebooks, which support development in Python, R, and Scala. DSX also includes R Studio - software by an IBM business partner which has been integrated in DSX. DSX environment connects to a Spark service, which provides highly scalable environment for running analytics. 

**Watson Machine Learning**
Watson Machine Learning (WML) service contains three types of capabilities: 
a. Online, batch, and streaming deployment of SparkML and Python scikit-learn models
b. Repository for models
c. Wizards for simplifying creation of SparkML models
WML is integrated in the DSX UI, and it's also accessible through APIs (Python, R, Scala) and via UI in the Bluemix WML service. 

**Spark Service**
Spark Service is included with DSX by default, but if the user wants to add additional processing power, they can connect DSX/WML projects to a Spark Service configured in Bluemix. 

**dashDB Bluemix Service**
Bluemix dashDB service, as well as many other types of cloud and on-premise data sources. DSX includes "Connector API" for over 20 data sources. Connector API simplifies and streamlines access to different types of data sources. If a data source is not supported by the Connector API, the standard data source connection approach (for example, a jdbc driver) can be used. Please note that Secure Gateway Bluemix service is required for accessing on-premise data sources. 

**Python Flask Bluemix Service**
After models are deployed in WML they can be acccessed via REST APIs. We created a sample client applicaiton in Python Flask, a popular Web programming API. Any on-premise or cloud application that can integrate with a REST API can invoke models deployed in WML. 

## Application and Use Case Overview
Our example implements a predictive model for telco churn. We chose telco churn as an example because it's easy to understand, and at the same time it implements frequently used analytics approach - a classification model to predict churn. 

The notebook that implements the use case provides more details about the use case and analytics implementation. 
 
## Project files
This project contains all the required files for building out the architecture and completing the tutorial.
1. Notebooks
2. Data
3. Python Flask application

## Run the reference application in IBM Cloud
To run the sample applications you will to complete several steps in DSX, WML, and optionally, dashDB and Spark Services.  

### Step 1: Environment Setup

#### Prerequisites

1. Sign up for Data Science Experience (https://datascience.ibm.com/) and Bluemix. Make sure to use the same userid (otherwise Bluemix services will not be available in DSX)
2. In Bluemix, provision the following services
- Watson Machine Learning: https://console.ng.bluemix.net/catalog/services/ibm-watson-machine-learning/?env_id=ibm:yp:us-south
- dashDB for Analytics: https://console.ng.bluemix.net/catalog/services/dashdb-for-analytics?env_id=ibm:yp:us-south&taxonomyNavigation=apps
- Spark: https://console.ng.bluemix.net/catalog/services/apache-spark?env_id=ibm:yp:us-south&taxonomyNavigation=apps
- Python Flask (use TelcoChurnDemo for the name): https://console.ng.bluemix.net/catalog/starters/python-flask?env_id=ibm:yp:us-south&taxonomyNavigation=apps

**EL TODO: add screenshots**
### Step 2: Review the notebook, deploy and test model in WML
1. Log in to Data Science Experience: https://datascience.ibm.com/
2. Create a new project with a name * * Data Science Use Case * * (it's important to use this name because the sample Notebook references it)
3. Swtich to the **Data Assets** tab and load the data files - churn.csv and customer.csv
4. Use the "+" icon to create the Notebook from file. Browse to * *TecloChurn.ipynb* * file included with this project
5. Click on the Edit (pencil) icon to enter the edit mode. Follow instructions in the notebook.

### Step 3 (optional): Connect project to a new Bluemix Spark Service

### Step 4 (optional): Switch data source to dashDB service

### Step 5: Test deployed service with a Python Flask application
Test with 
