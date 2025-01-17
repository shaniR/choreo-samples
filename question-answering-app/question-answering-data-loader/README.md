# Choreo Question Answering Bot Example - Data Loader

Welcome to the Choreo Question Answering Bot Example! This application is designed to help you get familiar with the Choreo platform and its features.

## Overview

This program demonstrates loading documentation data from a Google Spreadsheet and populating a Pinecone vector database with the content and their embeddings. The data can be used by the Question Answering Bot in order to find sources and context to answer questions. The sample uses Azure OpenAI to generate embeddings for the content.

### Getting Started

To use the example:
1. **Create Azure OpenAI embedding model deployment and obtain the keys and configs**: [Create deployments](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/create-resource?pivots=web-portal) for the Azure OpenAI embedding model and obtain the following configs for the Azure OpenAI service.
    ```
    API Key
    API Base URL
    API Version
    Deployment ID of the embedding model
    ```
2. **Setup the Google Spreadsheet with Document Data**: 
    - Visit [Google API Console](https://console.developers.google.com), click **Create Project**, and follow the wizard to create a new project.
    - Go to **APIs and Services** and on the **Credentials** tab, click **Create credentials** and select **Service Account**.
    - Provide the name and description for the service account and click **Done**.
    - In created service account, go to the **Keys** tab, click **Add Key** and select **Create new key**.
    - Select **JSON** as the key type and click **Create**. The JSON file with the credentials will be downloaded to your machine.
    - Create a new Google Sheet in your account and add your document content as two columns for **title** and **content** (similar to the example data given in `./data/example_data.csv`).
    - Obtain the SheetID from the URL and Worksheet Name.
3. **Set up the Pinecone Vector Database**:
    - Sign up and log in to [Pinecone](https://www.pinecone.io/).
    - Create an index (set the configurations for the **OpenAI/text-embedding-ada-002** model) and obtain the environment name.
    - Click on `API Keys` and create an API key.
4. **Fork the Repository**: Fork this repository to your GitHub account.
5. **Clone Your Forked Repository**:
   ```
   git clone [URL of your forked repository]
   ```
6. Log into [Choreo](https://console.choreo.dev/)
7. Create a project in choreo and create a new componant of type **Manual Task** by providing the repository path for the `question-answering-data-loader`, with the `Python` buildpack and `3.10.x` as the Python version.
8. Add the contents of the generate Google Service Account credentials as a configmap and specify the mount path as `/config/gs_credentials.json`.
9. Configure the following configs as environment variables in the component.
    ```
    SHEET_ID: <Google Sheet ID>
    WORKSHEET_NAME: <Google Sheet Name>
    PINECONE_API_KEY: <Pinecone API Key>
    PINECONE_INDEX_NAME: <Pinecone Index Name>
    PINECONE_ENVIRONMENT: <Pinecone Environment Name>
    OPENAI_API_KEY: <Azure OpenAI API Key>
    OPENAI_API_BASE: <Azure OpenAI API Base URL>
    EMBEDDING_MODEL: <Azure OpenAI Embedding Model Deployment ID>
    ```
10. Build and execute the manual task.

### Contribution & Feedback

We greatly value community insights:

- **Contribute**: Got a new example or an enhancement? We'd love to incorporate it.
- **Feedback**: Encounter issues or have suggestions? Please raise them under this repository's [issues section](https://github.com/wso2/choreo-samples/issues).
