# RH Dynatrace Escape Room 101 Setup

# This repo hosts instructions for Ansible/EDA and Dynatrace setup

## Prerequisites

- For EasyTravel app - RHEL VM or EC2 instance (or similar on Azure/GCP) for EasyTravel app
- For EasyTrade setup - OpenShift cluster with an account that has admin privileges
- Ansible Automation Platform (AAP) and Event Driven Ansible (EDA) instances (requires AAP >= 2.4)
- Access to a Dynatrace tenant

### Escape Room Lab Setup
- For the RH environment, you can provision the following RH Demo Platform catalog item: [Event-driven Ansible Demo](https://demo.redhat.com/catalog?item=babylon-catalog-prod/enterprise.event-driven-ansible.prod) OR provision your own Ansible and EDA instances
- For the Dynatrace environment, please have access to a Dynatrace SaaS tenant. 

## Reference App Setup for Observability

We have 2 options for deploying a reference app that can be used for Dynatrace observability and simulating problem events that can be detected by Dynatrace.
NOTE: The Dynatrace tenant and Ansible/EDA setup instructions in the following sections are using Easytrade as the reference app but they apply to the Easytravel app as well.

- Set up Easytravel app on RHEL VM
  1. [Deploy](https://docs.dynatrace.com/docs/shortlink/oneagent-linux-install) Dynatrace OneAgent 
  2. Here's a [guide](https://community.dynatrace.com/t5/Start-with-Dynatrace/easyTravel-Documentation-and-Download/m-p/181271) for deploying the Easytravel app on RHEL
  3. Alternatively, you can also refer to the [OneAgent](https://github.com/gvorg/rh-dt-escape-room-101/blob/main/playbooks/dynatrace-oneagent-install.yml) and [Easytravel](https://github.com/gvorg/rh-dt-escape-room-101/blob/main/playbooks/easytravel-install.yml) install playbooks in this repo to automate the process via Ansible

- Set up Easytrade app on OpenShift
  1. [Deploy](https://docs.dynatrace.com/docs/shortlink/installation-openshift-operatorhub#installation) the Dynatrace Certified Operator from the OpenShift OperatorHub
  2. Here's a [guide](https://github.com/gvenkatx/easytrade?tab=readme-ov-file#red-hat-openshift-instructions) for deploying the app on OpenShift
 

## Dynatrace Tenant Setup

- Token for Accessing Dynatrace API from Ansible/EDA
  - See [Dynatrace API Token Creation](https://docs.dynatrace.com/docs/shortlink/api-authentication) guide for details
  - ![Screenshot 2024-10-25 at 3 35 33 PM](https://github.com/user-attachments/assets/750cc0c0-0482-4441-80e2-173935703824)


### For Easytravel App

- Web application detection
  - ![Screenshot 2025-04-24 at 2 24 54 PM](https://github.com/user-attachments/assets/a02262da-38a2-4ac5-9db6-9cee7b7a30db)
  - ![Screenshot 2025-04-24 at 2 32 13 PM](https://github.com/user-attachments/assets/7832c84e-936f-42d2-a672-0e5ebfc34934)


- Web application user tagging for identiying user sessions by names
  - ![Screenshot 2025-04-24 at 2 34 59 PM](https://github.com/user-attachments/assets/9f41f6a5-6ca8-4aa9-82b8-850bce1beac9)
  - ![Screenshot 2025-04-24 at 2 36 43 PM](https://github.com/user-attachments/assets/be629611-0cdd-478d-be37-a0caf27fbf98)
  - ![Screenshot 2025-04-24 at 2 37 22 PM](https://github.com/user-attachments/assets/0c1dc721-f979-44a3-9326-48ed7613e446)



### For Easytrade App

- Web application detection
  - ![dt_webapp_detection_1](https://github.com/user-attachments/assets/3860e263-080b-41d9-bea8-912bc97da2f7)
  - ![dt_webapp_detection_2](https://github.com/user-attachments/assets/f93aa8fd-1c06-4ade-90ab-be394ab77d70)
 
- Web application tagging
  - ![dt_webapp_tag](https://github.com/user-attachments/assets/d742d464-c0fa-4ba6-80b8-d5fea268d644)

- Web application user tagging for identiying user sessions by names
  - ![dt_webapp_usertag_1](https://github.com/user-attachments/assets/6e571d92-42bb-4340-8022-7053a237e52c)
  - ![dt_webapp_usertag_2](https://github.com/user-attachments/assets/79f73b96-0f71-4f8a-b48a-e6e0ef848abb)
  - ![dt_webapp_usertag_3](https://github.com/user-attachments/assets/09e87498-6279-408c-8e43-27d83abcbca5)
  - ![dt_webapp_usertag_4](https://github.com/user-attachments/assets/55279a1d-47ab-41c3-9990-db7a8047dec1)
  - ![dt_easytravel_usertag](https://github.com/user-attachments/assets/58599bf3-f2c3-4058-bb04-37aee2d30b04)



## Red Hat Ansible Automation Controller Setup


- Create EDA Token
  - Refer to this [link](https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.4/html/event-driven_ansible_controller_user_guide/eda-set-up-token#eda-set-up-token) for setting up an access token for EDA to access Ansible Automation Controller. NOTE: If you are using the [Event-driven Ansible Demo](https://demo.redhat.com/catalog?item=babylon-catalog-prod/enterprise.event-driven-ansible.prod catalog item on RH demo platform, this token is already setup for you.

- Create Project
  - ![aap_project](https://github.com/user-attachments/assets/c117575a-8b94-4a40-af50-1edbe6cb9aed)


- Create Templates
  - ![aap_break_template_1](https://github.com/user-attachments/assets/85395f6a-2bd7-4e2b-a3ab-6910931e5303)
  - ![aap_fix_template_1](https://github.com/user-attachments/assets/9234b999-a915-46ab-a2d6-4fb6f5490f26)


- ![aap_job_templates](https://github.com/user-attachments/assets/7e5002e3-141b-4c28-a631-caf9d3e10a2e)



## Event Driven Ansible Controller Setup
The Ansible EDA setup currently only refers to the [Dynatrace Event Source Plugin](https://github.com/Dynatrace/Dynatrace-EventDrivenAnsible/blob/main/extensions/eda/plugins/event_source/dt_esa_api.py). The instructions will be updated to also include the Dynatrace Webhook Plugin once we update everything to use AAP 2.5.

- Create Decision Environment
  - ![eda_de_2](https://github.com/user-attachments/assets/19b911bf-f648-4826-b6bb-f9792e914d06)


- Create Project
  -  ![eda_project](https://github.com/user-attachments/assets/697a6968-a0d7-46ad-b89f-205cbac50241)


- Create Rulebook Activation
  - The example shown here is using the Dynatrace Event Source Plugin. The repo will be updated shortly with an example for using a Webhook.
  -  ![eda_rulebook_1](https://github.com/user-attachments/assets/226d4da9-c54c-4246-9a51-6f7be7f7cb96)
  -  ![eda_rulebook_2](https://github.com/user-attachments/assets/4e26616c-9a8e-427a-8cfd-8cdd94df03bb)


## Problem Scenario Setup for Easytravel

Reference link to Problem Patterns that can be generated for Easytravel: [https://community.dynatrace.com/t5/Start-with-Dynatrace/Available-easyTravel-problem-patterns/m-p/181674]
1. First you need to have the website started http://<easytravel URL>:8094/main -> UEM -> standard 
2. Login to EasyTravel web shop using different credentials in private browser tab, and purchase trips to create some sessions. Always close the browser tab to make the session end after each purchase. Credentials are e.g. bian/bian, alex/alex, anna/anna, fa/fa, demi/demi http://<easytravel URL>:9079/easytravel/home
3. Use AAP job template to break the easytravel website - [easytravel-break](https://github.com/gvorg/rh-dt-escape-room-101/blob/main/playbooks/easytravel-break.yml)
4. Login as maria/maria and make purchase fail in webshop, and make sure there is trace in jobs that AAP fixed it. You probably need to hit the purchase button tens of times quickly to make the dynatrace raise the problem. It often takes some minutes for DT to raise the problem report
5. Ensure from AAP logs EDA & AAP fixed the website.
This is mandatory, participants are hunting for these traces

