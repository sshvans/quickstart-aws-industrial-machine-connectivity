# Industrial Machine Connectivity (IMC) AWS Quick Start

## Introduction
The IMC framework is designed to enable customers and partners to get data from their assets to AWS in a simple, structured process so they can rapidly realize the business value that is derived from that data. The IMC Quick Start has the capability to convert customers’ existing asset hierarchy definitions (i.e. factory, lines, machines, tags, etc.) defined in partner edge applications like Inductive Automation’s Ignition Server or PTC’s KEPServerEX to the equivalent asset hierarchy within AWS IoT SiteWise. This capability is enabled by the Asset Model Converter (AMC), a component of the IMC architecture. With asset hierarchies defined within IoT SiteWise, customer data can be ingested continuously to the AWS cloud and all the pertinent metadata is readily accessible for applications that can be built on top of the IMC kit architecture which will use that data to deliver business value, such as asset condition monitoring or root cause analysis (RCA) dashboards applications.

## IMC Kit Overview
![IMC-Kit Overview](/documentation/images/IMC-Overview.png)

## What is included in this Quick Start?
The IMC kit will include the software (launched via AWS CloudFormation) and a list of compatible edge hardware devices that together can connect a customer's industrial assets to the AWS cloud. The industrial asset data and its meta-data (i.e. asset/asset tag hierarchy information) are made available with the IMC kit, enabling application builders to focus their efforts on value add development like building applications and dashboards for customers.

## IMC Kit Architecture
![IMC-Kit Overview](/documentation/images/IMC-Architecture.png)

## Deployment Types

The IMC kit can be deployed in 3 configurations:

### Virtual Deployments
**Type 1: Virtual Deployment:** The virtual deployment is intended for demonstration, training and evaluation of the Kit’s capabilities. EC2 instances will be launched to simulate edge gateway hardware but in all other respects the experience will mirror that of the real physical deployment. This deployment mode relies on simulated tag values generated by the partner edge software. There are no physical PLCs or sensors that are being connected.

### Physical Deployments
Physical deployment of the IMC kit enables users to deploy edge software (i.e. AWS IoT Greengrass and partner edge software) on physical industrial PCs that are ready to connect to physical devices (I.e. PLCs)/historians/SCADA systems on the customers plant floor. The physical deployment has two flavors:

**Type 2: Physical - Greenfield:** AWS IoT Greengrass and the partner edge software will be running on a single industrial PC.

**Type 3: Physical - Brownfield:** AWS IoT Greengrass will run standalone on an industrial PC and will connect to partner edge software application that is already running on the customers premises (i.e. on a VM in the server room of a manufacturing plant). We assume our access to the hardware is limited or non-existent, and our ability to reconfigure the Edge Software Application Server is limited to additive changes only.

**Note:**
The type of deployment (Virtual or Physical) determines whether to use physical edge hardware (Physical industrial PCs) or virtual edge hardware (EC2) and how connectivity and security is configured. All other cloud-based resources are largely the same.

## Getting Started

**STEP 1**
To get started, review the master user guide document to learn about the IMC kit its components and capabilities.

**STEP 2**

Once you decide which of the 3 deployment types you would like to launch, click the link to the appropriate deployment user guide below and follow the instructions. Ensure that you are preparing pre-requisite resources and launching the CloudFormation stack in one of the 3 supported regions for the IMC kit:
-	us-east-1
-	us-west-2
-	eu-west-1

1. Virtual
    - User Guide Document: [“IMC - Virtual Deployment User Guide”](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Virtual%20Deployment%20User%20Guide.docx)
2. Physical - Greenfield
    - User Guide Document: [“IMC - Physical - Greenfield User Guide”](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Physical-Greenfield%20Deployment%20User%20Guide.docx)
3. Physical - Brownfield
    - User Guide Document: [“IMC - Physical - Brownfield User Guide”](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Physical-Brownfield%20Deployment%20User%20Guide.docx)

## Data Flow Options

In addition to the Virtual/Physical edge hardware distinction, the IMC kit supports three types of data flow architectures. Each type outlines different methods of data ingestion from the edge environment into the AWS Cloud. 

- Option 1: Edge Software Application OPCUA Server -> AWS IoT SiteWise
    - In this variant, we have the AWS Greengrass SiteWise Connector configured to connect to the Edge Software Application OPCUA Server. All telemetry data will flow directly into AWS IoT SiteWise.
- Option 2a: Edge Software Application Server -> AWS IoT Core
    - In this variant, the Edge Software Application Server has some kind functionality to connect to IoT Core via MQTT. All telemetry data is pushed from the Edge Software Application Server to AWS IoT Core, and from there usually pushed to S3 or a similar data lake for processing.
- Option 2b: Edge Software Application Server -> AWS Greengrass Core -> IoT Core -> S3
    - Option 2b is almost identical to option 2a, except we instead have the Edge Software Application Server pushing MQTT data messages to AWS Greengrass Core first, and then those messages are forwarded on to AWS IoT Core.

## Resources
See the appendix in the ['IMC - Master User Guide.docx'](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/develop/documentation/IMC%20-%20Master%20User%20Guide.docx) below for additional information about:
1.	Creating new AMC drivers
    - This is relevant for partners or customer that wish to integrate a new edge software application with the IMC kit
2.	Artifacts
    - List of artifacts that are required to launch the CloudFormation templates
3.	AMC-Approved DynamoDB Format
    - Details the format of the 2 DynamoDB tables that the AMC uses to store the SiteWise asset model and asset information needed to provision resources in SiteWise.
4.	Add a line and a device to an Ignition Project
    - These instructions show a user how to add an additional device to an Ignition Server project and how that new device will be provisioned in AWS IoT SiteWise via the AMC.

## FAQs
Frequently asked questions are addressed in the **'FAQ'** section in the specific deployment guide you are using:
1. [Virtual Deployment](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Virtual%20Deployment%20User%20Guide.docx)
2. [Physical-Greenfield Deployment](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Physical-Greenfield%20Deployment%20User%20Guide.docx)
3. [Physical-Brownfield Deployment](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Physical-Brownfield%20Deployment%20User%20Guide.docx)

## Troubleshooting

For information on troubleshooting the IMC kit CloudFormation stack launch and operation, see the **'Troubleshooting'** section in specific deployment user guide you are using:
1. [Virtual Deployment](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Virtual%20Deployment%20User%20Guide.docx)
2. [Physical-Greenfield Deployment](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Physical-Greenfield%20Deployment%20User%20Guide.docx)
3. [Physical-Brownfield Deployment](https://github.com/aws-quickstart/quickstart-aws-industrial-machine-connectivity/raw/master/documentation/IMC%20-%20Physical-Brownfield%20Deployment%20User%20Guide.docx)