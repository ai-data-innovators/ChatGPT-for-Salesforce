# ChatGPT for Salesforce

Detailed guidance on configuring ChatGPT as a conversational interface for Salesforce.

## Leveraging ChatGPT to Streamline Salesforce Workflows

Integrating ChatGPT with Salesforce grafts a multi-modal intelligent user interface onto a powerful business system. This configuration is accessible enough for any tech-savvy individual to implement, yet unlocks significant capabilities and future possibilities.

Key Features:
* Multi-modal input: Interact with ChatGPT using text, images, or voice while reading data from and writing data to Salesforce.
* Enhanced mobile experience: Enables a flow experience for mobile users, such as field sales teams, to effortlessly write notes, create tasks, and generate leads.
* Simple configuration: Utilizes Salesforce's standard Connected App feature and ChatGPT's GPT builder, available to all Plus, Team, or Enterprise subscribers.
* Prompt Engineering: Supports interactive improvement through prompt engineering.
* API Integration: Leverages APIs available for modern SaaS (Software as a Service) software.

While the initial setup is straightforward, it initiates an iterative process to incorporate AI into routine business workflows and drive towards a more intelligent, responsive, and efficient systems environment for business professionals.

## Step by Step Implementation Guide

At high level, there are only three steps: 

* Configure a Salesforce Connected App
* Create a Custom GPT in ChatGPT
* Validate, Share, and Keep Improving Your GPT

### Configure a Salesforce Connected App

1. Log in to your Salesforce org as an administrator. 
2. Go to **Setup** > **Apps** > **App Manager**.
3. Click "**New Connected App**" in the upper right corner.
4. Fill in the basic information:
   - Connected App Name: "ChatGPT Integration" (Or any name you like)
   - API Name: This will auto-fill
   - Contact Email: Your email address
5. Check "**Enable OAuth Settings**"
6. Set the Callback URL to a temporary URL (e.g., https://login.salesforce.com/services/oauth2/callback). Later we will comeback to change this to an URL that ChatGPT will provide. 
8. Add these OAuth Scopes:
   - **Manage user data via API (api)**
   - **Perform requests at any time (refresh_token, offline_access)**

Now the screen looks like this
![Salesforce Connected App for GPT](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/Salesforce-Connected-App-for-GPT-Configuration.png)

9. Save the connected app. After save, click the "Continue" buttom to go to the connected app screen, which has a "**Manage Consumer Details**" button. Click the button to get the "**Consumer Key and Secret**". 
10. Note down the following infomation needed for ChatGPT configuration. 
  * **Consumer Key**
  * **COnsumer Secret**
  * Your Salesforce **subdomain** from the brower address bar. For example, my page URL is "https://ai-experience-dev-ed.develop.my.salesforce.com/...", so, my subdomain is "ai-experience-dev-ed.develop.my.salesforce.com"

### Create a Custom GPT in ChatGPT

To configure a GPT with an action to interact with Salesforce:

1. Go to chat.openai.com and click on "**Explore GPTs**" in the left sidebar.
2. Click "**Create a GPT**" and give it a name like "**Salesforce Companion**".
3. In the configuration, add a **description** explaining its purpose.
4. In the "**Instructions**" section, add guidelines for how the GPT should interact with Salesforce. You can download a sample one from here: …

By now, the ChatGPT screen loolks like this: 

![ChatGPT GPT Configuration Screen Part 1](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/Custom-GPT-Salesforce-Companion-Configuration.png)

5. Under "**Actions**", click "**Create new action**".
6. For **Authentication**, select “**OAuth**”, and set the following parameters: 
  * Client ID = the Consumer Key from the Salesforce connected app
  * Client Secret = the Consumer Secret from the Salesforce connected app
  * Authorization URL = https://<your subdomain>/services/oauth2/authorize
  * Token URL = https://<your subdomain>/services/oauth2/token
  * Scope: api, refresh_token, offline_access
  * Token Exchange Method: Default (POST request)
7. For OpenAPI schema, you can download a [sample YAML file](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/sample-salesforce-api-spec-for-custom-gpt.yaml). 
  * Use a text editor to replace "ai-experience-dev-ed.develop.my.salesforce.com" with your subdomain. There are a few places to change in the initial version. 
  * Copy and paste the resulting file to the schema textbox. (The "Import from URL" function does not work at time of writing. )

The **Add actions** screen look like this: 

![Custom GPT Add Actions Screen](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/Custom-GPT-Add-Actions.png)

8. Click the "Create" on the top right corner of the screen. On the "Share GPT" popup, select "Only me". At this point, we are not ready to share the GPT yet.
9. Now, you will find a "**Callback URL**" on the custom GPT Configure screen. Get this URL, revisit the Salesforce connected app to replace the placeholder value with this URL. After the change, take a good rest before coming back to test the custom GPT, as the redirct URL change can take quite a while in my experience.
10. Finally, you can test the GPT. Here are a few simple test prompts I haved used:
  * Please get my accounts
  * Please get the contacts on account ACME. 
  * Please get my opportunities
  * Now let's create a note
  * Let's create a task

### Validate, Share, and Keep Improving Your GPT

When testing your ChatGPT-Salesforce integration:

1. Start with simple queries like "Find the latest opportunity for [Account Name]" or "Create a task for [Contact Name]".
2. Pay attention to how the GPT formulates API requests and handles responses.
3. Refine your prompts and instructions based on the results.
4. Gradually test more complex scenarios, such as updating records or running reports.
