# Microsoft-Feature-Ready-Talent-Project
https://sites.google.com/mmit.edu.in/corona-omicron-chatbot/home

QnA Maker or summary of project
Bot Framework v4 QnA Maker bot sample. This sample shows how to integrate Multiturn and Active learning in a QnA Maker bot with ASP.Net Core-2. Click here to know more about using follow-up prompts to create multiturn conversation. To know more about how to enable and use active learning, click here.

This bot has been created using Bot Framework, it shows how to create a bot that uses the QnA Maker Cognitive AI service.

The QnA Maker Service enables you to build, train and publish a simple question and answer bot based on FAQ URLs, structured documents or editorial content in minutes. In this sample, we demonstrate how to use the QnA Maker service to answer questions based on a FAQ text file used as input.

Concepts introduced in this sample
The QnA Maker Service enables you to build, train and publish a simple question and answer bot based on FAQ URLs, structured documents or editorial content in minutes. In this sample, we demonstrate -.how to use the Active Learning to generate suggestions for knowledge base. -.how to use the Multiturn experience for the knowledge base .

Prerequisites
- Follow instructions here to create a QnA Maker service.

Follow instructions here to create multiturn experience.
Follow instructions here to import and publish your newly created QnA Maker service.
Update appsettings.json with your kbid (KnowledgeBase Id), endpointKey and endpointHost. QnA knowledge base setup and application configuration steps can be found here.
(Optional) Follow instructions here to set up the QnA Maker CLI to deploy the model.
Create a QnAMaker Application to enable QnA Knowledge Bases
QnA knowledge base setup and application configuration steps can be found here.

Configure Cognitive Service Model
Create a Knowledge Base in QnAMaker Portal.
Import "smartLightFAQ.tsv" file, in QnAMaker Portal.
Save and Train the model.
Create Bot from Publish page.
Test bot with Web Chat.
Capture values of settings like"QnAAuthKey" from
"Configuration" page of created bot, in Azure Portal.
Updated appsettings.json with values as needed.
Use value of "QnAAuthKey" for setting "QnAEndpointKey".
Capture KnowledgeBase Id, HostName and EndpointKey current published app
Try Active Learning
Once your QnA Maker service is up and you have published the sample KB, try the following queries to trigger the Train API on the bot.
Sample query: "light"
You can observe that, Multiple answers are returned with high score.
Try Multi-turn prompt
Once your QnA Maker service is up and you have published the sample KB, try the following queries to trigger the Train API on the bot.
Sample query: "won't turn on"
You can notice a prompt, included as part of answer to query.
To try this sample
Clone the repository

git clone https://github.com/Microsoft/botbuilder-samples.git
In a terminal, navigate to samples/csharp_dotnetcore/49.qnamaker-all-features

Run the bot from a terminal or from Visual Studio, choose option A or B.

A) From a terminal

# run the bot
dotnet run
B) Or from Visual Studio

Launch Visual Studio
File -> Open -> Project/Solution
Navigate to samples/csharp_dotnetcore/49.qnamaker-all-features folder
Select QnABot.csproj file
Press F5 to run the project
Microsoft Teams channel group chat fix
Goto Bot/QnABot.cs
Add References
using Microsoft.Bot.Connector;
using System.Text.RegularExpressions;
Modify OnTurnAsync function as:
public override async Task OnTurnAsync(ITurnContext turnContext, CancellationToken cancellationToken = default)
    {
        // Teams group chat
        if (turnContext.Activity.ChannelId.Equals(Channels.Msteams))
        {
            turnContext.Activity.Text = turnContext.Activity.RemoveRecipientMention();
        }
        
        await base.OnTurnAsync(turnContext, cancellationToken);

        // Save any state changes that might have occurred during the turn.
        await ConversationState.SaveChangesAsync(turnContext, false, cancellationToken);
        await UserState.SaveChangesAsync(turnContext, false, cancellationToken);
    }
Testing the bot using Bot Framework Emulator
Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots on localhost or running remotely through a tunnel.

Install the Bot Framework Emulator version 4.3.0 or greater from here
Connect to the bot using Bot Framework Emulator
Launch Bot Framework Emulator
File -> Open Bot
Enter a Bot URL of http://localhost:3978/api/messages
Deploy the bot to Azure
See Deploy your C# bot to Azure for instructions.

The deployment process assumes you have an account on Microsoft Azure and are able to log into the Microsoft Azure Portal.

If you are new to Microsoft Azure, please refer to Getting started with Azure for guidance on how to get started on Azure.

Further reading
[Active learning Documentation][al#1]
Bot Framework Documentation
Bot Basics
Azure Bot Service Introduction
Azure Bot Service Documentation
msbot CLI
Azure Portal
Deployment Url : https://sites.google.com/mmit.edu.in/corona-omicron-chatbot/home
