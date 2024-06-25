# Workshop: Securing polygot, gen ai applications in Kubernetes with Calico

## Welcome

This sample demo app consists of a group of containerized microservices that can be easily deployed into an Azure Kubernetes Service (AKS) cluster. This is meant to show a realistic scenario using a polyglot architecture, event-driven design, and common open source back-end services (eg - RabbitMQ, MongoDB). The application also leverages OpenAI's GPT-3 models to generate product descriptions. 
This can be done using either Azure OpenAI or OpenAI.



In this workshop you will use Calico Cloud to secure a polygot, microservices architecture that uses OpenAI.

This workshop can be used with AKS, EKS, or GKE.

In today's highly interconnected and digital landscape, ensuring the security of your Kubernetes clusters is an absolute necessity.
This workshop provides you with the essential knowledge and skills to strengthen your cluster's defenses thoroughly, guaranteeing the safeguarding of vital workloads and sensitive information.
It enables you to tailor security measures to suit your specific needs and keeps you at the forefront of cybersecurity in a swiftly evolving environment.

### Time Requirements

The estimated time to complete this workshop is 60-120 minutes.

### Learning Objectives

- Learn how to set up workload access controls with microsegmentation
- Learn how to use global network policies for namespace (or tenant) isolation
- Implement DNS-based egress access control with network sets and network policy
- Use the breadth of Calico's observability features to monitor, visualize and troubleshoot issues within the cluster

## Workshop Environment Preparation

> :warning: **For this workshop, you are expected to have access to a previously created AKS, EKs, or GKE cluster.**

- Please, follow the instructions on the repository below if you don't have it ready: 

  [Calico Cloud on AKS - Workshop Environment Preparation](/setup/aks-setup.md)
  [Calico Cloud on EKS - Workshop Environment Preparation](/setup/eks-setup.md)
  [Calico Cloud on GKE - Workshop Environment Preparation](/setup/gke-setup.md)

- You will need an [OpenAI](https://openai.com/) account

## Modules

This workshop is organized in sequential modules. One module will build up on top of the previous module, so please, follow the order as proposed below.

Module 1 - [Connect the cluster to Calico Cloud](/mod/module-1-connect-calicocloud.md)  
Module 2 - [Deploy an Application](/mod/module-2-deploy-application.md)  
Module 3 - [Workload Microsegmentation](/mod/module-3-namespace-isolation.md)  
Module 4 - [Container Security and Calico Security Events](/mod/module-4-security-events.md)  
Module 5 - [Web Application Firewall](/mod/module-5-waf.md)  
Module 6 - [Egress Gateway and Azure Firewall](/mod/module-6-egress-gateway-azure-firewall.md)  

--- 

### Useful links

- [Project Calico](https://www.tigera.io/project-calico/)
- [Calico Academy - Get Calico Certified!](https://academy.tigera.io/)
- [O’REILLY EBOOK: Kubernetes security and observability](https://www.tigera.io/lp/kubernetes-security-and-observability-ebook)
- [Calico Users - Slack](https://slack.projectcalico.org/)

**Follow us on social media**

- [LinkedIn](https://www.linkedin.com/company/tigera/)
- [Twitter](https://twitter.com/tigeraio)
- [YouTube](https://www.youtube.com/channel/UC8uN3yhpeBeerGNwDiQbcgw/)
- [Slack](https://calicousers.slack.com/)
- [Github](https://github.com/tigera-solutions/)
- [Discuss](https://discuss.projectcalico.tigera.io/)

> **Note**: The workshop provides examples and sample code as instructional content for you to consume. These examples will help you understand how to configure Calico Cloud and build a functional solution. Please note that these examples are not suitable for use in production environments.