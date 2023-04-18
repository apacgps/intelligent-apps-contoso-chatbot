# Intelligent Apps Contoso Chatbot
This sample application is forked from [Azure-Samples/cosmosdb-chatgpt](https://github.com/Azure-Samples/cosmosdb-chatgpt).

This sample application combines Azure App Service, Azure Cosmos DB with Azure OpenAI Service with a Blazor Server front-end for an intelligent chat bot application that shows off how you can build a simple chat application.

![image](https://user-images.githubusercontent.com/79892729/231650919-9087a50a-f8fe-4c64-b228-fb2ce858b651.png)

## Features

This application has individual chat sessions which are displayed and can be selected in the left-hand nav. Clicking on a session will show the messages that contain
human prompts and AI completions. 

When a new prompt is sent to the Azure OpenAI Service, some of the conversation history is sent with it. This provides context allowing GPT model to respond
as though it is having a conversation. The length of this conversation history can be configured from appsettings.json
with the `OpenAiMaxTokens` value that is then translated to a maximum conversation string length that is 1/2 of this value.

Please note that the model used by this sample has a maximum limit of tokens. Tokens are used in both the request and reponse from the service. Overriding the maxConversationLength to values approaching maximum token value could result in completions that contain little to no text if all of it has been used in the request.

The history for all prompts and completions for each chat session is stored in Azure Cosmos DB. Deleting a chat session in the UI will delete it's corresponding data as well.

The application will also summarize the name of the chat session by asking the GPT model to provide a one or two word summary of the first prompt. This allows you to easily identity different chat sessions.

Please note this is a sample application. It is intended to demonstrate how to use Azure App Service, Azure Cosmos DB and Azure OpenAI Service together. <b>It is not intended for production or other large scale use.</b>

## Getting Started

### Prerequisites

- Azure Subscription
- Subscription access to Azure OpenAI service. Start here to [Request Acces to Azure OpenAI Service](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUOFA5Qk1UWDRBMjg0WFhPMkIzTzhKQ1dWNyQlQCN0PWcu)
- Visual Studio, VS Code, or some editor if you want to edit or view the source for this sample.


### Installation

1. Clone this repository to your own GitHub account.
2.  Depending on whether you deploy using the ARM Template or Bicep, modify this variable in one of those files to point to your fork of this repository, "webSiteRepository": "https://github.com/apacgps/intelligent-apps-contoso-chatbot.git" 
3. Use the Deploy to Azure button below, and modify this README.md file to change the path for the Deploy To Azure button to your local repository.
4. If you deploy this application without making either of these changes, you can update the repository by disconnecting and connecting an external git repository pointing to your clone.


The provided ARM or Bicep Template will provision the following resources:
1. Azure Cosmos DB account with database and container at 400 RU/s. This can optionally be configured to run on the Cosmos DB free tier if available for your subscription.
2. Azure App service. This will be configured for CI/CD to your cloned GitHub repository. This service can also be configured to run on App Service free tier.
3. Azure Open AI account. You must also specify a name for the deployment of the GPT model which is used by this application.

Note: You must have access to Azure Open AI Service from your subscription before attempting to deploy this application.

All connection information for Azure Cosmos DB and Azure OpenAI Service is zero-touch and injected as environment variables in the Azure App Service instance at deployment time. 

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fapacgps%2Fintelligent-apps-contoso-chatbot%2Fmain%2Fazuredeploy.json)

### Quickstart

1. After deployment, go to the resource group for your deployment and open the Azure App Service in the Azure Portal. Click the web url to launch the website.
2. Click + New Chat to create a new chat session.
3. Type your question in the text box and press Enter.

## Clean up

To remove all the resources used by this sample, you must first manually delete the deployed model within the Azure OpenAI service. You can then delete the resource group for your deployment. This will delete all remaining resources.

## Resources
- [Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/overview)
- [Azure Cosmos DB + Azure OpenAI ChatGPT Blog Post Announcement](https://devblogs.microsoft.com/cosmosdb/)
- [Azure Cosmos DB Free Trial](https://aka.ms/TryCosmos)
- [OpenAI Platform documentation](https://platform.openai.com/docs/introduction/overview)
- [Azure OpenAI Service documentation](https://learn.microsoft.com/azure/cognitive-services/openai/)
