# Project Overview

Build a CI/CD pipeline to automate the deployment of a machine learning microservice API using Flask. Set up a GitHub repository with structured scaffolding, incorporating a Makefile, requirements.txt, and application code. Use GitHub Actions for Continuous Integration by running linting, testing, and installation workflows. Integrate Azure Pipelines for Continuous Delivery to deploy the Flask app to Azure App Services. Demonstrate DevOps and ML engineering skills with a final demo showcasing the operationalization of machine learning models in a cloud environment.


## Project Plans

The project plan is structured into milestones, covering Flask API development, ML model integration, CI/CD implementation, testing, and deployment. 

- The [trello board](https://trello.com/b/yB1P1XJD/buildcicdpipeline) track tasks in 3 categories: To Do, In Progress and Done.
- The [spreadsheet](https://docs.google.com/spreadsheets/d/1U11YbFkv5H8b5wT21PZTcDiYmlsPfOksCUsgEl4DDH0/edit?usp=sharing) timeline outlines key deadlines and responsibilities.


This ensures efficient progress, clear accountability, and a smooth deployment to Azure.

### Project architecture

```mermaid
graph TD;
    A["GitHub Repository (Flask App Code)"] --> B["GitHub Actions (CI)"];
    B -->|Runs Tests & Linting| C["Azure Pipelines (CD)"];
    C -->|Deploys to Azure & More Tests/Linting| D["Azure App Service"];
    D -->|Serves Predictions| E["Prediction Service"];

```

### Azure Cloud Shell Setup

1. Launch Azure Cloud shell env and create ssh-keys. Upload these keys to Github account. [ref](https://www.youtube.com/watch?v=Z8uRw6N5TGY&t=84s)

```bash
ssh-keygen -t rsa
cat /home/shekhar/.ssh/id_rsa.pub
```

2. Clone the repo to Azure (use SSH)
  
  <img width="458" alt="image" src="https://github.com/user-attachments/assets/93c87388-a6a4-4e3e-a3ac-f4f7dd7e74d6" />

3. Project cloned into Azure Cloud shell
<img width="482" alt="image" src="https://github.com/user-attachments/assets/0ca6b2be-86a7-45fd-9ca4-97f9a3904f06" />

4. Create makefile, requirements.txt in the Github repo.

5. Create Python virtual environment 
<img width="493" alt="image" src="https://github.com/user-attachments/assets/e9805a1b-777c-4611-81b3-8463866d988a" />

```bash
python3 -m venv ~/.Build_CI_CD_pipeline
source ~/.Build_CI_CD_pipeline/bin/activate
```

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

1. Enable GitHub Actions in the GitHub UI.  [ref](https://www.youtube.com/watch?v=U29oRwnkASw&t=16s)
2. Add the pythonapp.yml in the GitHub Actions workflow.
3. Verify remote tests pass in GitHub Actions UI
<img width="878" alt="image" src="https://github.com/user-attachments/assets/b61a9801-65d6-4f91-8381-f2a31815e170" />

4. The GitHub Actions build passed.

<img width="919" alt="image" src="https://github.com/user-attachments/assets/de074d45-69ad-4800-8a0b-f46462d97cf2" />

### CD on Azure

This is the final step that invloves setting up Azure Pipelines to deploy the Flask application on Azure App Services.
(This case, Azure Pipelines are used to deploy CD, which can be done with GitHub Actions as well.)

Enable source control integration, select the Azure Pipelines to build provider, and finally configure the App Services permissions.

![image](https://github.com/user-attachments/assets/e04b185e-10bd-4216-83aa-e8c5f71f88a6)

1. Get the starter [code](https://github.com/udacity/nd082-Azure-Cloud-DevOps-Starter-Code/tree/master/C2-AgileDevelopmentwithAzure/project/starter_files) and add to the repo. Git clone and put the **flask-sklearn** folder inside the main branch.
2. When launching Azure Pipelines, creating a resource group is an important step. 
It helps organize and manage all the resources required for the pipeline.
Create a resource group (in case, you still have tag-policy, please do not forget to add tags).

```bash
az group create -l northeurope -n "cicd-rg"
```

<img width="800" alt="image" src="https://github.com/user-attachments/assets/d92a82ee-6791-4a56-b9ac-e9c287769fdf" />


3. Before proceeding, ensure that you are in the **Azure Cloud Shell**, located in the correct **project directory** (this case flask-sklearn), and also make sure, you've **activated Python** using the `source` command.

Now, create the web app. To do so, run the following command: (it takes sometime)
Azure 1st checks if that webapp exists, if not, it creates it.
(the name can be anything, here it is **house-price-pred-app**)

[Location codes](https://gist.github.com/ausfestivus/04e55c7d80229069bf3bc75870630ec8)

```bash
az webapp up --runtime PYTHON:3.9 --sku F1 --logs --location northeurope --name house-price-pred --resource-group "cicd-rg" 
```

![image](https://github.com/user-attachments/assets/80579ed4-794a-42af-a2d8-0faf8bae4a87)




Please go to Azure portal (GUI) and search for **house-price-pred**:

<img width="940" alt="image" src="https://github.com/user-attachments/assets/12fe5bdf-13ff-436c-b888-735b5f8e618b" />

Check if the UI is running:

<img width="352" alt="image" src="https://github.com/user-attachments/assets/9a9f9f90-04b2-456f-8a7f-8f2c294929e1" />


4. **Prediction is 2.43** (not 20.xxx)

<img width="552" alt="image" src="https://github.com/user-attachments/assets/930bf380-66df-4241-ae4e-e8f24d8ed0fe" />


5. Check log file
   
```bash
https://house-price-pred.scm.azurewebsites.net/api/logs/docker
```

![image](https://github.com/user-attachments/assets/aa3f9c24-3e2a-4a75-a0fb-e012e16dcc35)

6. Build PAT token so that we can authenticate Azure DevOps services with VM on Azure. 

<img width="935" alt="image" src="https://github.com/user-attachments/assets/6cc3e131-ae3e-4945-ae3f-7c5d14a0e8d0" />

[ref](https://www.youtube.com/watch?v=jzX2fOaf67w&t=136s)

(A VM created on Azure can connect to Azure DevOps Agent Pool by help of PAT)

Please note that you can also Microsoft-hosted agents. (That case PAT and VM are not necessary)
Below it shows when you need self-hosted agents.

<img width="521" alt="image" src="https://github.com/user-attachments/assets/47288845-20f8-4bf0-8adf-a401028d326e" />

7. While running Azure pipeline for the 1st time, you might encounter this error:

<img width="952" alt="image" src="https://github.com/user-attachments/assets/3b7aded6-f6f1-4b04-9538-86f7d06e5d5d" />

Please fill up the form and request for approval from MS:

<img width="782" alt="image" src="https://github.com/user-attachments/assets/201d7c72-eedf-4eda-ae70-251970e8a062" />

**This is the reason you need to set up self-hosted agents.**

8. Create Self-Hosted Agent(VM), Configure the agent (VM), Install Agent services, Verify myAgentPool has the agent (VM) Online.
So the agent has been successfully registered in this myAgentPool

![image](https://github.com/user-attachments/assets/6ae5cd27-023f-419b-8d4f-81d509c6731d)


9. Simple run of Azure Pipelines (job is successful)

<img width="949" alt="image" src="https://github.com/user-attachments/assets/79ad9e37-25b8-4af1-93b4-8e63a8910e6f" />



10.  Deployed webapp **house-price-pred** to Azure via Azure pipeline ( chose **master branch** for the same)

<img width="806" alt="image" src="https://github.com/user-attachments/assets/d6b53d8e-c9c1-4bb5-8894-8d4250225120" />

<img width="605" alt="image" src="https://github.com/user-attachments/assets/76a86ba8-e363-4954-904b-c27aa11ff3fe" />

(During deployment of webapp, the Azure devops pipeline will ask for Permission)



## Enhancements

1. Modify the Flask App to have new endpoints ( adding postal code, type of house etc.)
2. Use different ML tasks to 

## Demo 

[youtube](https://youtu.be/BBx5CQ4mvWs)
