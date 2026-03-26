# How to build a virtual assistant with watsonx Assistant
We will be creating an action-based assistant to take coffee orders.

## Creating an IBM Cloud Account

### For Students

**How to create an IBM Cloud Account**

Read: https://github.com/academic-initiative/documentation/blob/main/academic-initiative/how-to/How-to-create-an-IBM-Cloud-account/readme.md

Please complete the prereq session in this readme first, i.e.

1. You must register for the SkillsBuild program with your university email address
   https://github.com/academic-initiative/documentation/blob/main/academic-initiative/how-to/How-to-register-with-the-IBM-Academic-Initiative/readme.md

2. Request an IBM Cloud feature code
   https://github.com/academic-initiative/documentation/blob/main/academic-initiative/how-to/How-to-request-and-IBM-Cloud-Feature-Code/readme.md

### For Regular Users

1. Go to this link and create an account: https://cloud.ibm.com/registration.
2. If you already have an account, go to https://cloud.ibm.com and click **Log in** on the top right of the page to continue.

## Provisioning Your Assistant

You have two options to create and work with watsonx Assistant:

### Option 1: watsonx Assistant (Standalone)

1. Once logged in, click on `Catalog` in the top bar (next to the search area).
2. Search for `Assistant`.
3. Under the `AI / Machine Learning` Category, click on `watsonx Assistant`.
4. Scroll down and make sure the `Lite` Plan is selected for the free plan.
5. Click `Create`.
6. Click on `Launch watsonx Assistant`.
7. You will be taken directly to the assistant builder interface.

### Option 2: watsonx Orchestrate (Trial)

watsonx Orchestrate is an AI-powered platform that enables you to build, deploy, and manage intelligent agents that automate business tasks. It supports workflow automation and agentic workflows, allowing agents to execute multi-step processes, integrate with enterprise systems, and take actions based on user requests. Additionally, assistants such as watsonx Assistant can be integrated as collaborator agents within orchestrated solutions.

Learn more: https://www.ibm.com/products/watsonx-orchestrate

**Creating a watsonx Orchestrate Trial Instance:**

1. Once logged in, click on `Catalog` in the top bar (next to the search area).
2. Search for `Orchestrate`.
3. Under the `AI / Machine Learning` Category, click on `watsonx Orchestrate`.
4. Scroll down and select the `Trial` Plan.
5. Click `Create`.
6. Wait for your trial instance to be provisioned (this may take a few minutes).
7. Once ready, click on `Launch watsonx Orchestrate`.

**Creating Your First Assistant in watsonx Orchestrate:**

1. From the watsonx Orchestrate home page, click the **hamburger menu** (☰) in the top left corner.
2. Scroll down and click on **Assistant builder** at the bottom of the menu.
3. The assistant creation wizard will open automatically.
4. **Name and Language:**
   - Give your assistant a name (e.g., "Coffee Shop Assistant")
   - Add a description (e.g., "An assistant to help customers order coffee, tea and soft drinks")
   - **Important:** Choose your language (e.g., US English). Watson uses this language to understand user utterances and map them to the action that best matches. The example phrases you provide (customer says sentences) should align with this language.
   - Click **Next**
5. **Assistant Details:**
   - For "Where will this assistant be used?", select **Web**
   - For "What is your role?", select **N/A (I am a student)**
   - For "What is your level of experience?", select **Developer**
   - For "What do you want to build?", select **Not sure at this time**
   - Click **Next**
6. **Validate and create:**
   - Review your assistant name
   - Click **Next**
   - Click **Create** to create your assistant

Your assistant is now created and you're ready to start creating your first action!

**Note:** Whether you choose Option 1 or Option 2, the assistant builder interface and the steps to create actions are the same. watsonx Orchestrate simply provides additional features for automation, agentic capabilities, and workflow orchestration alongside your assistant.

## Understanding Actions in watsonx Assistant

watsonx Assistant uses an **action-based** approach to build conversational flows. Actions are goal-oriented tasks that your assistant can help users complete. Each action consists of:

- **Customer starts with**: Example phrases that trigger the action
- **Steps**: A sequence of questions and responses to gather information
- **Variables**: Information collected from the user
- **Conditions**: Logic to handle different scenarios

For more information, see: https://www.ibm.com/docs/en/watsonx/watson-orchestrate/base?topic=assistants-building-your-ai-assistant-actions#build-actions-from-scratch

## Creating Your First Action: Order a Drink

1. In the watsonx Assistant interface, click the **Build actions** tile or click **Actions** in the left navigation menu.
2. Click **Create action**.
3. For your first action in watsonx Orchestrate, select **Custom-built action** (Note: In standalone watsonx Assistant, this option may be called "Start from scratch").
4. A pop-up window titled **"New action"** will appear with the subtitle **"What does your customer say to start this interaction?"**
5. Enter a sample sentence in the text field, for example:

   ```
   I would like to order a coffee please
   ```
6. Click **Save** to create the action.

### Add More Sample Sentences

Now you need to add more example phrases so Watson can better understand different ways customers might order a drink.

1. Click in the **"Customer starts with"** box at the top left of the action editor.
2. Add the following sample sentences one by one (press Enter after each):
   - I need some caffeine
   - order espresso
   - a cappuccino would be lovely
   - a latte please

These example phrases help Watson understand the various ways customers might express their intent to order a drink. The more examples you provide, the better Watson becomes at recognizing similar requests.

### Step 1: Ask What They Want to Drink

After having entered the sample sentences, you are ready to create the conversation flow.

1. Click on the **1st step** in the **Conversation steps** section on the left side of the screen.
2. In the **Assistant says** field, enter:

   ```
   What would you like to drink?
   ```
3. Click **Define customer response**.
4. Select **Options** as the response type.
5. Add the following options with synonyms:
   - **coffee** (synonyms: cafe, java, brew)
   - **tea** (synonyms: chai)
   - **soft drink** (synonyms: soda, pop, cola)
6. Click **Apply** to save the options.
7. The response will be automatically saved to an action variable named to something like `1. [text]`.

### Step 2: Ask How Many Cups

1. Click **New step** to add another step.
2. In the **Assistant says** field, type:

   ```
   How many cups of 
   ```
3. Place your cursor at the end of the text.
4. Click the **fx** button (insert variable) to add an action variable to the response.
5. Select the `1. [text]` action variable from the previous step.
6. Continue typing to complete the sentence (make sure to start with a space):
   ```
    would you like?
   ```
   The final text should read: "How many cups of [drink_type variable] would you like?"
7. Click **Define customer response**.
8. Select **Number** as the response type.
9. This will be saved to an action variable named to something like `2. [text]`.

### Step 3: Confirm the Order

1. Click **New step** to add a confirmation step.
2. In the **Assistant says** field, type:

   ```
   Okay, so you would like 
   ```
3. Click the **fx** button and select the action variable from Step 2 (e.g., `2. [text]`).
4. Continue typing:

   ```
    (space)
   ```
5. Click the **fx** button again and select the action variable from Step 1 (e.g., `1. [text]`).
6. Complete the sentence by typing:

   ```
   . Is this correct?
   ```
   The final text should read: "Okay, so you would like [quantity variable] [drink_type variable]. Is this correct?"
7. Click **Define customer response**.
8. Select **Options** as the response type.
9. Add the following options with synonyms:
   - **Yes** (synonyms: correct, right, yep, yeah, sure)
   - **No** (synonyms: nope, incorrect, wrong)
10. Click **Apply** to save the options.
11. This will be saved to an action variable named to something like `3. [text]`.

### Step 4: Handle "No" Response - Start Over

1. Click **New step** to handle when the customer says "No".
2. Look for the **Is taken** dropdown at the top of the step.
3. Change the dropdown from **Is taken** to **with conditions**.
4. The correct action variable from Step 3 is already selected. Make sure the value is set to **No**.
5. In the **Assistant says** field, enter:

   ```
   No problem. Let's try again then...
   ```
6. Click **And then** at the bottom of the step.
7. Select **Re-ask previous steps**.
8. Choose to re-ask Step 1 (What would you like to drink?). Step 2 and 3 will automatically be selected as well.
9. Click **Apply**.

### Step 5: Handle "Yes" Response - Complete the Order

1. Click **New step** to handle when the customer says "Yes".
2. Look for the **Is taken** dropdown at the top of the step.
3. Change the dropdown from **Is taken** to **with conditions**.
4. The correct action variable from Step 3 is already be selected. Make sure the value is set to **Yes**.
5. In the **Assistant says** field, type:

   ```
   Okay, 
   ```
6. Click the **fx** button and select the quantity action variable from Step 2.
7. Type a space, then click the **fx** button again and select the type of drink action variable from Step 1.
8. Complete the sentence by typing:

   ```
    coming right up! ☕️☕️
   ```
   The final text should read: "Okay, [quantity variable] [drink_type variable] coming right up! ☕️☕️"
9. Click **And then** at the bottom of the step.
10. Select **End the action**.

## Testing Your Action

1. Click the **Preview** button (chat bubble icon) in the bottom right corner.
2. Type one of your example phrases, such as "I would like to order a coffee please".
3. Follow the conversation flow:

   - Select a drink type
   - Enter a quantity
   - Confirm your order
4. Test both "Yes" and "No" paths to ensure the logic works correctly.

**CONGRATULATIONS!!** 🎉 👍

You successfully created an action-based assistant! Your coffee ordering bot can now:
- Understand multiple ways customers ask for drinks
- Collect drink type and quantity
- Confirm orders before processing
- Handle corrections when customers change their mind


## [Optional] Deploying Your Assistant

### Web Chat Integration

1. Click on **Integrations** in the left navigation menu.
2. Select **Web chat**.
3. Click **Open** to configure the web chat.
4. Customize the appearance:
   - Change the accent color
   - Add your coffee shop name
   - Upload a logo
   - Customize the greeting message
5. Click **Save and exit**.
6. Copy the embed code from the **Embed** tab.
7. Paste the code into your website's HTML before the closing `</body>` tag.

### Testing the Web Chat

You can use the provided `web-chat-example.html` file:

1. Open `web-chat-example.html` in a text editor.
2. Replace the `<!-- INSERT EMBED SCRIPT HERE -->` comment with your embed code.
3. Save the file.
4. Open the file in your web browser.
5. Start chatting with your assistant!
