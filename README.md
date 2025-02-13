# Project Overview

Build a CI/CD pipeline to automate the deployment of a machine learning microservice API using Flask. Set up a GitHub repository with structured scaffolding, incorporating a Makefile, requirements.txt, and application code. Use GitHub Actions for Continuous Integration by running linting, testing, and installation workflows. Integrate Azure Pipelines for Continuous Delivery to deploy the Flask app to Azure App Services. Demonstrate DevOps and ML engineering skills with a final demo showcasing the operationalization of machine learning models in a cloud environment.


## Project Plans

The project plan is structured into milestones, covering Flask API development, ML model integration, CI/CD implementation, testing, and deployment. 

- The [trello board](https://trello.com/b/yB1P1XJD/buildcicdpipeline) track tasks in 3 categories: To Do, In Progress and Done.
- The [spreadsheet](https://docs.google.com/spreadsheets/d/1U11YbFkv5H8b5wT21PZTcDiYmlsPfOksCUsgEl4DDH0/edit?usp=sharing) timeline outlines key deadlines and responsibilities.


This ensures efficient progress, clear accountability, and a smooth deployment to Azure.



### Azure Cloud Shell Setup

1. Launch Azure Cloud shell env and create ssh-keys. Upload these keys to Github account. [ref](https://www.youtube.com/watch?v=Z8uRw6N5TGY&t=84s)
2. Clone the repo to Azure (use SSH)
  
  <img width="458" alt="image" src="https://github.com/user-attachments/assets/93c87388-a6a4-4e3e-a3ac-f4f7dd7e74d6" />

3. Project cloned into Azure Cloud shell
<img width="482" alt="image" src="https://github.com/user-attachments/assets/0ca6b2be-86a7-45fd-9ca4-97f9a3904f06" />

4. Create makefile, requirements.txt in the Github repo.

5. Create Python virtual environment 
<img width="493" alt="image" src="https://github.com/user-attachments/assets/e9805a1b-777c-4611-81b3-8463866d988a" />

6. Run make all

<img width="695" alt="image" src="https://github.com/user-attachments/assets/1787aec4-40b1-49a5-aafe-e97ce672b241" />

7. All the test cases should pass

<img width="949" alt="image" src="https://github.com/user-attachments/assets/5f5c79cb-064f-49ac-9de7-46618773e86c" />


###  Configure GitHub Actions

Configure GitHub Actions to test your project upon change events in GitHub. Ensure continuous integration (CI) is performed remotely by setting up automated tests whenever code is checked into a Git-based repository. Set up both a SaaS build service and the necessary configuration files to define the build process. Use GitHub Actions as the CI service to automate testing and validation.

DevOps best practices by integrating GitHub Actions into your project. 
This step finalizes the CI process, preparing the project for the next phase: Continuous Delivery.
A push event to GitHub triggers a GitHub Actions container, which executes a series of predefined commands.

![image](https://github.com/user-attachments/assets/979b6d72-7b7e-4c69-a006-e70039a4e819)

1. Create **pythonapp.yml**
2. Enable GitHub Actions in the GitHub UI. 
