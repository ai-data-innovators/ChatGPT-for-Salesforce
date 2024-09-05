# ChatGPT for Salesforce Configuration Guide

Detailed guidance on configuring ChatGPT as a conversational interface for Salesforce.

## Leveraging ChatGPT as an Intelligent Interface for Salesforce

Integrating ChatGPT with Salesforce adds a multi-modal intelligent user interface onto a powerful business system. This configuration is accessible enough for any tech-savvy individual to implement, yet it unlocks significant capabilities and future possibilities.

Key Features:
* Multi-modal input: Interact with ChatGPT using text, images, or voice while reading data from and writing data into Salesforce.
* Enhanced mobile experience: Enables a seamless experience for mobile users, such as field sales teams, to effortlessly write notes, create tasks, and generate leads.
* Simple configuration: Utilizes Salesforce's standard Connected App feature and ChatGPT's GPT builder, available to all Plus, Team, or Enterprise subscribers.
* Prompt Engineering: Supports interactive improvement through prompt engineering.
* API Integration: Leverages APIs available for modern SaaS (Software as a Service) software.

While the initial setup is straightforward, it begins an iterative process to incorporate AI into routine business workflows, driving towards a more intelligent, responsive, and efficient systems environment for business professionals.

## Screenshots of Custom GPT Field Force Companion

Below are screenshots of the Custom GPT "Field Force Companion" in action. The images demonstrate how ChatGPT can be used to query Salesforce data and create new records directly within the interface.

<p float="left">
  <img src="https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/ChatGPT-GPT-Field-Force-Companion-Queries.png" alt="Query Salesforce in ChatGPT" width="45%" />
  <img src="https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/ChatGPT-GPT-Field-Force-Companion-Create-Records.png" alt="Create Salesforce Records in ChatGPT" width="45%" />
</p>

## Step-by-Step Implementation Guide

At a high level, there are only three steps: 

* Configure a Salesforce Connected App
* Create a Custom GPT in ChatGPT
* Share and Improve Your GPT

### Configure a Salesforce Connected App

1. Log in to your Salesforce org as an administrator. 
2. Go to **Setup** > **Apps** > **App Manager**.
3. Click "**New Connected App**" in the upper right corner.
4. Fill in the basic information:
   - Connected App Name: "ChatGPT Integration" (Or any name you like)
   - API Name: This will auto-fill
   - Contact Email: Your email address
5. Check "**Enable OAuth Settings**"
6. Set the Callback URL to a temporary URL (e.g., https://login.salesforce.com/services/oauth2/callback). Later, we will come back to change this to a URL that ChatGPT will provide. 
7. Add these OAuth Scopes:
   - **Manage user data via API (api)**
   - **Perform requests at any time (refresh_token, offline_access)**

The screen should now look like this:
![Salesforce Connected App for GPT](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/Salesforce-Connected-App-for-GPT-Configuration.png)

8. Save the connected app. After saving, click the "Continue" button to go to the connected app screen, which has a "**Manage Consumer Details**" button. Click the button to get the "**Consumer Key and Secret**". 
9. Note down the following information needed for ChatGPT configuration. 
  * **Consumer Key**
  * **Consumer Secret**
  * Your Salesforce **subdomain** from the browser address bar. For example, if your page URL is "https://ai-experience-dev-ed.develop.my.salesforce.com/...", then your subdomain is "ai-experience-dev-ed.develop.my.salesforce.com."

### Create a Custom GPT in ChatGPT

To configure a GPT with an action to interact with Salesforce:

1. Go to chat.openai.com and click on "**Explore GPTs**" in the left sidebar.
2. Click "**Create a GPT**" and give it a name like "**CRM Companion**".
3. Add a **description** explaining its purpose. Keep it simple and concise. 
4. In the "**Instructions**" section, add instructions on how the GPT should interact with Salesforce. You can copy and paste this tested sample: [sample-gpt-instructions-for-salesforce-integration](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/sample-gpt-instructions-for-salesforce-integration.md)

At this stage, the ChatGPT screen looks like this: 

![ChatGPT GPT Configuration Screen](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/Custom-GPT-CRM-Companion-Configuration.png)

5. Under "**Actions**", click "**Create new action**".
6. For **Authentication**, select “**OAuth**”, and set the following parameters: 
  * Client ID = the Consumer Key from the Salesforce connected app
  * Client Secret = the Consumer Secret from the Salesforce connected app
  * Authorization URL = https://{your subdomain}/services/oauth2/authorize
  * Token URL = https://{your subdomain}/services/oauth2/token
  * Scope: api, refresh_token, offline_access
  * Token Exchange Method: Default (POST request)
7. For OpenAPI schema, you can download this tested sample: [sample-salesforce-openapi-spec-for-custom-gpt.yaml](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/sample-salesforce-openapi-spec-for-custom-gpt.yaml). 
  * Use a text editor to replace "ai-experience-dev-ed.develop.my.salesforce.com" with your subdomain. There are a few places to change in the initial version. 
  * Copy and paste the resulting file to the schema textbox. (The "Import from URL" function does not work at the time of writing. )

The **Add actions** screen looks like this: 

![Custom GPT Add Actions Screen](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/images/Custom-GPT-Add-Actions.png)

8. Click "Create" in the top right corner of the screen. On the "Share GPT" popup, select "Only me". At this point, we are not ready to share the GPT yet.
9. Now, you will find a "**Callback URL**" on the custom GPT Configure screen. Get this URL, revisit the Salesforce connected app to replace the placeholder value with this URL. After making the change, rest a while before testing the custom GPT, as the redirect URL update may take some time to take effect.
10. Finally, you can test the GPT. Here are a few simple test prompts you can use:
  * Please get my accounts
  * Please get the contacts on account ACME. 
  * Please get my opportunities
  * Now let's create a note
  * Let's create a task

There is no need for perfection as AI is making rapid progress. We can focus on the possibilities of AI and practical ways to get things done better. 

### Share and Improve Your GPT

1. To share your custom GPT, go back to its configuration screen and click on the "**Share**" button. The "Share GPT" popup will prompt you to set privacy policy URLs for public actions. Here is a sample generated by ChatGPT: [sample-public-actions-privacy-policy](https://github.com/ai-data-innovators/ChatGPT-for-Salesforce/blob/main/sample-public-actions-privacy-policy.md)
2. Once published, you can share your GPT with friendly colleagues, encouraging them to explore and provide feedback.
3. You can continue improving your GPT with simple prompt engineering. 

### Final Words

I hope you found this interesting to try. I'd appreciate any feedback using this simple form [ChatGPT-for-Salesforce Feedback Form](https://forms.gle/ukDhe3ryVT2X1DXQ9). 
