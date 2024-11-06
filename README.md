# RAG-Setup
This README contains instructions to set up RAG in a partner's PoC account

RAG - Retrieval Augmented Generation https://www.ibm.com/architectures/hybrid/genai-rag

## Provision document store

### IBM Cloud Databases for Elasticsearch:

1. Install ElasticSearch using the Terraform scripts located [here](https://github.com/ibm-build-lab/terraform-elasticsearch-setup)

1. Download ELSER model into Elasticsearch database

    a. Open Kibana (url link and pwd from Step 1, userid=admin)

    b. From main menu on top left choose **Machine Learning** → **Trained Models**

    c. On the far right on line item `.elser_model_2_linux-x86_64` model, you should see a **Download** link.  Take that, once the status says it’s downloaded, select **Deploy**
 1. Ingest documents into Elasticsearch: 

    See https://github.com/ibm-build-lab/wxd-file-ingestion-utilities for options

###  Watson Discovery
Create a Project, upload and train documents.  For the actions to search **Watson Discovery** instead of **ElasticSearch**, you will need to change the "No matches" assistant action to call the `Query WD + LLM` action instead of `Query ES + LLM`

## Provision **watsonx.ai**

  a. Go to https://dataplatform.cloud.ibm.com/wx/home?context=wx, and follow login prompts.  

  b. Create a project, open project. 

  c. Associate Services - create and associate **Watson Studio** and **Watson Machine Learning** instances.  **Note**, you will need to change the plan to **Essentials** of greater for the **Machine Learning **instance or you will run out of tokens. You may also need to create and associate a **Cloud Object Storage** instance.

## Provision the RAG-LLM-Service on Code Engine

Go to https://github.com/ibm-build-lab/RAG-LLM-Service/tree/main/codeengine-setup for steps to do this

## Provision watsonx Assistant Plus plan

Create an assistant to connect to **RAG-LLM-Service**.  Create a custom extension for **RAG-LLM-Service** and upload the actions located in https://github.com/ibm-build-lab/RAG-LLM-Service/tree/main/watsonx-assistant-setup.  See https://github.com/ibm-build-lab/RAG-LLM-Service/blob/main/watsonx-assistant-setup/README.md for more information and detailed steps.

Optional: Create a different assistant to connect up Integrated Conversational Search to test differences. See https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=assistants-conversational-search

## Test and tweak prompts

You can change the `question`, `llm_instructions`, `llm_params.model_id`, and the other `llm_params` variables to improve the search

## Fork and customize RAG-LLM-Service if need be depending on engagement

If you want to add functionality to the **RAG-LLM-Service**, follow the instructions [here](https://github.com/ibm-build-lab/RAG-LLM-Service/tree/main?tab=readme-ov-file#contributing)

## Additional documentation: 

API documentation for Watsonx Assistant https://cloud.ibm.com/apidocs/assistant-v2
