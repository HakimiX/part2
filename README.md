# Maintenance and SLA Status

## Hand-over

The focus is on technical documentation. The purpose of a technical document is to show the development process. It includes information about the initial software requirements, system overview, technical requirements, system configuration, setup and dependencies. 

The technical documentation should allow other developers to operate our systems, report issues and provide feedback. Our technical document provides an overview of the Hacker news clone system requirements and a lead-in to the system architecture, components, dataflow and workflow. In addition, we have a section about Issue submission and system access. [Technical Documentation](https://github.com/HakimiX/Documentation)

It was our responsibility to operate Group J’s system. Their technical document was missing information about system architecture, proper description of data flow process and a detailed issue submission. Generally, their technical document was not very detailed and we didn’t feel well equipped to maintain their system. For example, we got a HTTP Status 404 – Not Found Error whenever we tried to access Group J’s backend through the browser. [Group J's backend](http://46.101.111.112:8080/lsd-backend/)

![Text]()

## Service-level Agreement

The service-level agreement is a contract that defines the agreement between a customer and service provider. It specifies what the customer will receive and clarifies what performance standards the service provider is obligated to meet. Our service-level agreement contains a description of what the contract includes and service agreements. The following service parameters were the responsibility of the service provider:

* __Uptime__ – applies to servers, cloud services or other parts of the system that are vital. Guaranteed at least 95% uptime. 

* __CPU Usage__ – applies to amount of actively used CPU, as percentage of total available CPU. Amount of used CPU time (CPU used, CPU wait etc.). Alert if CPU is above 70% for 5 min. 

* __Group A support response time__ – applies to how long it takes Group A to respond when we raise a request for support. Respond to critical problems within 24 hours. 

We did not have any disagreements about the service-level agreement. Our service-level agreement was written in a spirit of partnership. We were sure that Group A would do everything possible to rectify every issue. 

The service-level agreement was supposed to contain information about system monitoring using Grafana/Prometheus. Unfortunately, we were not able to setup Grafana/Prometheus properly. Group A could not comply with our service-level agreement, because we were not able to configure monitoring. Our monitoring problems will be explained in the following section. 

## Monitoring

Monitoring is crucial for DevOps (Development Operations). It makes it possible to see what is happening in your system at any given time. It gives you an overview of system resources currently used such as CPU, Memory, storage etc. The main purpose of monitoring is detecting problems, notifying possible issues and preventing them. 

As mentioned earlier, we were not able to setup monitoring for our system. We made use of Docker and were able to install Grafana and Prometheus. They were both exposed on their ports 3000 and 9090. 

![Text]()

Then we configured the Prometheus.yml file to point at 165.227.136.184 which is our Hacker News application. We also configured the scrape target to be Prometheus at localhost:9090. 

![Text]()

We installed the latest node exporter from [Prometheus](https://prometheus.io/download/#node_exporter), and exposed it on port 9100. Everything looked correct and we could see that everything was running on their respective ports. 

![Text]()

However, when we navigated to Prometheus at `165.227.136.184:9090/targets` we encountered node exporter errors such as `GET http://165.227.136.184:9100/metrics: dial tcp` and `165.227.136.184:9100: i/o timeout`. The Prometheus endpoint worked as intended besides the node exporter errors. 

![Text]()

Grafana also worked fine, and we were able to get basic HTTP metrics by connecting Grafana to Prometheus. Since we were not able to expose node exporter metrics, we could not configure Grafana to show metrics such as, uptime, storage, CPU, memory etc. 

![Text]()

We could not understand what the problem was, because we created new droplets on digital ocean to test Grafana/Prometheus and it worked fine. Node exporter metrics were exposed on port 9100 and we were able to show CPU, memory and storage metrics on Grafana. We applied the same steps to our Hacker News application, but it didn’t work because of the earlier mentioned node exporter errors. We tried everything possible to fix this, but we were not successful. Below is the metrics we needed: 

![Text]()

We have been very frustrated by this problem and are disappointed that we could not set up monitoring. Monitoring has been crucial for the service-level agreement, maintenance and generally development operations. 

## Maintenance and Reliability


