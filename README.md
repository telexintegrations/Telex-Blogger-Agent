# Telex Blogger Agent V1.0

## Overview
The **Telex Blogger** Agent is an AI-driven assistant that leverages the **Gemini API** to generate high-quality blog posts. Designed for seamless integration with Telex, it enables users to automate their **blog content** creation effortlessly.

## 1. Setting Up the Blogger Agent in Telex
To begin using the **Blogger Agent** in Telex, follow these steps:

### Step 1: Activate the Integration
1. **Log in** to your **Telex Organization**.
2. Navigate to the **Integrations** section.
3. Use the deployed URL of the integration JSON file below to **add the integration** to your organization:
   
   👉 **Integration URL:**
   ```
   https://telex-blogger-agent-qdp4.onrender.com/api/v1/telex-integration
   ```
4. Locate **Telex Blogger Agent** in the integration list and **Activate** it.
5. **Enter your channel’s webhook URL** in the settings field to allow the agent to send generated blog posts to your desired channel.
6. Click **Save** to complete the setup.

### Step 2: Generating Blog Content in Telex
Once the integration is active, you can use the **Blogger Agent** inside any **Telex channel**.

#### Triggering the Agent
You can generate a blog post by sending a message in Telex with an optional context provided:

👉 **Example Usage:**
```
"Generate a blog post on The Future of AI in Blogging"
```

The agent will **automatically send a structured blog post** to the webhook URL you provided during integration setup in the format of title, introduction, body and conclusion.

## 2. API Endpoints For Testing
The Blogger Agent provides two API endpoints:

---

### 1️⃣ Generate Blog Post (POST)
Generates a blog post based on user input.

👉 **Endpoint URL:**
```
POST https://telex-blogger-agent-qdp4.onrender.com/api/v1/blogger-agent/generate-blog
```

👉 **Request Body (JSON):**

Make sure to provide your channel webhook URL in the default payload. If not, the blog post will not be sent to the telex channel.

```json
{
  "message": "Generate a blog post on The Impact of AI on Content Writing",
  "settings": [
    {
      "label": "webhook_url",
      "type": "text",
      "required": true,
      "default": "https://your-webhook-url"
    }
  ]
}
```

👉 **Response:**

The response is a plain string containing the message you sent. The blog request is processed in the background.

```
Generate a blog post on The Impact of AI on Content Writing
```

Once the blog is generated, it will be **automatically sent** to the channel with the webhook URL you provided. This is done within a few seconds.

---

### 2️⃣ Telex Integration Configuration (GET)
Retrieves the integration.json.

👉 **Endpoint URL:**
```
GET https://telex-blogger-agent-qdp4.onrender.com/api/v1/telex-integration
```

👉 **Response:**

Retrieves the integration.json configuration for the agent. Example:

```
{"data":{"date":{"created_at":"2025-03-10","updated_at":"2025-03-10"},"descriptions":{"app_description":"AI-powered Blogging Assistant for Telex"},"integration_category":"AI & Machine Learning","integration_type":"modifier"}}
```


## 3. Project Structure
```
/Telex-Blogger-Agent
│── TelexBloggerAgent/                 
│   ├── Controllers/                    
│   │   ├── BloggerAgentController.cs   
│   │   ├── TelexIntegrationController.cs 
│   │   │
│   ├── Dtos/
│   │   ├── GenerateBlogDto.cs         
│   │   ├── TelexSettingsDto.cs         
│   │   │
│   ├── Helpers/                        
│   │   ├── GeminiSettings.cs          
│   │   ├── TelexSettings.cs           
│   │   │
│   ├── IServices/
│   │   ├── IBlogAgentService.cs        
│   │   ├── ITelexIntegrationService.cs 
│   │   │
│   ├── Services/                        
│   │   ├── BlogAgentService.cs        
│   │   ├── TelexIntegrationService.cs  
│   │   │
|   ├── appsettings.json
│   ├── Integration.json                
│   ├── Program.cs                     
│                              
│── README.md                           
│── .gitignore                          
│── Dockerfile                          
│── TelexBloggerAgent.sln              
```

## 4. Installing the Project Locally
To set up the project locally, follow these steps:

### Step 1: Clone the Repository
```sh
git clone https://github.com/telexintegrations/telex-blogger-agent.git
```

### Step 2: Install Dependencies
```sh
cd telex-blogger-agent
dotnet restore
```

### Step 3: Run the Application
```sh
dotnet run
```

## 5. Deployment
This application is **containerized using Docker** and deployed on **Render**.

### Current Deployment URL
👉 **Base URL:**  
```
https://telex-blogger-agent-qdp4.onrender.com
```

### Running with Docker
To deploy using **Docker**, use the following commands:

#### Build Docker Image
```sh
docker build -t telex-blogger-agent .
```

#### Run the Container
```sh
docker run -p 8080:8080 telex-blogger-agent
```

The app will be available at:
```
http://localhost:8080
```

## 6. Testing the Integration
To test if the **Blogger Agent** is working as expected:

1️⃣ **Send a Blog Generation Request**
```sh
curl -X POST "https://telex-blogger-agent-qdp4.onrender.com/api/v1/blogger-agent/generate-blog" \
     -H "Content-Type: application/json" \
     -d '{ "message": "Generate a blog post on How AI is Changing Blogging" }'
```

2️⃣ **Check Response**
Ensure the output contains the generated blog content.

3️⃣ **Verify in Telex**
Check your Telex channel to see if the generated blog post was sent to the **channel webhook URL** you provided.

## Conclusion
The **Telex Blogger Agent** simplifies blog writing by leveraging **AI-powered content generation**. With seamless integration into **Telex**, users can generate high-quality blog posts effortlessly.

🚀 **Start using it today and automate your blogging process!** 🚀

### Main Updates in This Version:
✅ **Webhook URL setting**: Users must provide a webhook URL to receive generated blog posts.  
✅ **Simplified commands**: No extra settings required in Telex commands.  
✅ **Automated posting**: Blog posts are sent directly to the configured Telex webhook.

