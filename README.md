
# Implementing Monitoring and Visibility for a Todo Microservices

### Application Background
You are tasked with implementing a monitoring and visibility solution for an existing set of microservices managing a todo application on AWS. The microservices have endpoints for creating, getting, listing, updating, and deleting todos. They have already been deployed on eu-west-3.

Your goal is to create a reporting/visibility solution using Prometheus and Grafana, or any other similar tool, to provide visibility into the logs and activities of the microservices.

Additionally, you need to create an AWS IAM role for the microservices to use.


### Deliverables:
- Configuration files for Prometheus and Grafana, if applicable.
- Documentation outlining the setup process and any additional considerations.
- Screenshots or links to Grafana dashboards showing metrics and logs from the microservices.
- AWS IAM role creation documentation.

### Additional Notes:
- Focus on simplicity, scalability, and maintainability in your implementation.
- Use existing AWS services and tools where possible to minimize complexity and cost.
- Ensure to work on the AWS region stated above.


## Implementation

![ToDo Service](image.png)

Implementing a monitoring and visibility solution for a set of microservices, particularly those running as AWS Lambda functions, involves a series of steps.
Below is an outlined comprehensive approach to achieve this.

1. **Utilize Amazon CloudWatch for AWS Lambda Monitoring**

    AWS Lambda functions automatically integrate with Amazon CloudWatch. Utilizing Amazon CloudWatch for AWS Lambda monitoring is a straightforward process, thanks to the tight integration between AWS services. CloudWatch automatically collects metrics, logs, and events from the AWS Lambda functions, allowing to monitor their performance and operational health in real-time


2. **Access Lambda Metrics in CloudWatch**
    - Log in to the AWS Console and open the CloudWatch service
    - Find the *Metrics* view in the CloudWatch dashboard
    - Within the *Metrics* view, select the `AWS/Lambda` namespace to view metrics related to each Lambda functions
    - Filter by Function Name to view specific data


![Lambda metrics](metrics.png)

3. **Access Logs**
   - In the AWS Management Console, go to the CloudWatch service.
   - Navigate to "Logs" in the sidebar.
   - Find the log group named /aws/lambda/<your-function-name> to access logs for  each specific Lambda function

![Lambda logs](logs.png)

4 **Set Up Grafana for Monitoring**

Grafana is a complete observability stack that allows you to monitor and analyze metrics, logs, and traces. It allows you to query, and visualize data.
Grafana supports cloudwatch as a data source, allowing us to visualize the Lambda logs and metrics collected by cloudwatch

*Steps*
- Within the `eu-west-3` region, launch an EC2 instance. Create a security group and add Port 22,80,and 3000 for our inbound rules pointing to all CIDR ranges.
-  Once the instance is lauched, SSH into it then, follow the instructions provided by Grafana to install it on the instance;
-  Download the GPG keys and add them to the trusted keys list.

    `wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add`
-  Now, add it to the Grafana repository.
-  `sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"` 
-  Once it has been added, we need to update the system.
-  `sudo apt update`
-  Install Grafana using command
-  `sudo apt install grafana`
-  Start Grafana: After Grafana is installed, you can start it by running the  following command:
-  `sudo systemctl start grafana-server`
-  Check the status of grafana by running following command:
-  `sudo systemctl status grafana-server`
- Access the Grafana web interface by navigating to the IP address of the EC2 instance in the web browser, followed by the default Grafana port (3000)
- log in to Grafana using the default credentials (admin/admin)
- Once you log in to grafana, navigate to  "Data sources"
- Choose AWS cloudwatch from the list osf available data sources
- Configure the data source by providing your AWS credentials ( Access and secret keys) and specify the `eu-west-3`
- Once that is done, select save and test


Here  is the link to the Grafana dashboard showing metrics and logs from the microservices.
Screen shots of the dashboards can also be found in the Grafana dashboards folder

http://13.38.245.145:3000/d/fdgxqie1vfp4we/lamda-functions-dashboard?orgId=1&from=1711380220316&to=1711553020316




