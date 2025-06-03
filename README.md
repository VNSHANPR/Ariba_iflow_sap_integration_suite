# Intgeration Suite iflow extarcting data form API AI and persisting in Datasphere OpenSQL schema
# Introduction

In this post I'm sharing some glimses from a recent project work involving data extraction from ARIBA API into SAP Datasphere OpenSQL schema using Integration suite with a basic dashboard in Analytics cloud. 

With the annoucement of SAP Business Data cloud (BDC), which is a fully managed SaaS solution that unifies and governs all SAP data and seamlessly connects with third-party data,  we will soon have standard Data Products & Insight Applications across SAP LoB solutions, and with that we will have direct access to such data assets without a need for such data integration as in this blog post. SAP has already started publishing these data products and these can be looked up here : SAP Data Products

In this post you get to see some highlights with screenshots on how SAP Integration suite can work with ARIBA APIs,  with end to end data modelling and visualization. Its quite relevant for customers with subscription of Integration Suite. 

For detailed implemenration of ARIBA API spend data extraction please refer this SAP Discovery mission which comes with Integration Suite iflows, sample SQL scripts to execute on Datasphere etc. 

While the discovery mission is very detailed , we will observe in the blog post the overall flow with sample implementation steps using a single iflow and if it leads to any help in your existing or sparks future project ideas that would be great. 

## ARIBA API 

I have used the Purchase orders buyer API which can tested using the free sandbox at api.sap.com 

## [ARIBA Network Purchase Orders buyer API](https://api.sap.com/api/purchase_orders/overview)


<img width="1060" alt="Screenshot 2025-05-29 at 5 53 42 PM" src="https://github.com/user-attachments/assets/7485f2be-cf15-4417-8ac9-0c5545fb14fc" />



Here is the sample Integration package with 3 iflows , a community version is available inside the 'Discovery integrations" tab, I have changed some parts of it as shown below :

Published ARIBA connection package in Integration suite : 


<img width="1209" alt="Screenshot 2025-05-30 at 1 22 40 PM" src="https://github.com/user-attachments/assets/13d23c2d-8d94-4dcd-abbd-7794c012cfd4" />

<img width="1492" alt="Screenshot 2025-05-30 at 12 44 40 PM" src="https://github.com/user-attachments/assets/c4f9b0bc-8764-4377-ac55-d400b2353fd8" />



## MODIFIED IFLOW : 

the modified version has following changes : :

General Splitter
Content modifier
JDBC receiver (OpenSQL schema of SAP Datasphere) 
If need you can download this from Github page : Download modified iflow

![Screenshot 2025-05-28 at 11 26 20 AM](https://github.com/user-attachments/assets/3b50d5e1-e718-47db-847c-93bf557ad5f0)




So the second iflow output_from_ARIBA is simply calling the first iflow using ProcessDirect and it gets deployed with an HTTP end point, which when queried triggers the first iflow "SAP ARIBA integration with SAP ARIBA APIs". The iflows are used to just show the mechanism of fast and direct communication between iflows using Process Direct, you can read more it here : [ProcessDirect](https://help.sap.com/docs/integration-suite/sap-integration-suite/processdirect-adapter)

in the screenshot you see that output_from_ARIBA iflow gets deployed with an address of /vinay/Ariba, this will reflect in the eventual endpoint when the iflow is deployed. 


<img width="859" alt="Screenshot 2025-05-30 at 1 19 05 PM" src="https://github.com/user-attachments/assets/0e9ef5a7-82cb-4195-a73e-9c0f7a64028e" />



Here we see the processDirect Adapter making an internal call to the first iflow, which gets deplyed with an address of : /Ariba/OpenAPI.

<img width="915" alt="Screenshot 2025-05-30 at 1 29 37 PM" src="https://github.com/user-attachments/assets/b5f18db2-21e0-46db-8430-5177de089843" />


Follow the SAP blog post here for more details : 
