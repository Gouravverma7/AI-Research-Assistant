# 🔎 Research Assistant

An AI-powered research assistant built with **Java Spring Boot** and a **Chrome Extension**. The application provides a browser-based research interface that communicates with a Spring Boot backend and uses **Google Gemini** to generate research-oriented responses.

## 🚀 Features

* 🤖 AI-powered research using Google Gemini
* 🌐 Chrome Extension interface
* 📌 Chrome Side Panel integration
* ⚡ Spring Boot REST API
* 🔗 Reactive HTTP communication using Spring WebClient
* 📤 Research query submission from the browser extension
* 📥 AI-generated research responses
* 🧩 Separation between controller, service, configuration, and entity layers
* 🧪 Spring Boot test setup

---

## 🏗️ Project Architecture

```text
Research Assistant
│
├── extension-frontend/
│   ├── manifest.json
│   ├── background.js
│   ├── sidepanel.html
│   ├── sidepanel.css
│   └── sidepanel.js
│
└── ResearchAssistant/
    ├── pom.xml
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   │   └── com/research/assistant/
    │   │   │       ├── config/
    │   │   │       │   └── WebClientConfig.java
    │   │   │       │
    │   │   │       ├── controller/
    │   │   │       │   └── ResearchController.java
    │   │   │       │
    │   │   │       ├── entities/
    │   │   │       │   ├── ResearchRequest.java
    │   │   │       │   └── GeminiResponse.java
    │   │   │       │
    │   │   │       ├── service/
    │   │   │       │   └── ResearchService.java
    │   │   │       │
    │   │   │       └── ResearchAssistantApplication.java
    │   │   │
    │   │   └── resources/
    │   │       └── application.properties
    │   │
    │   └── test/
    │       └── ...
    │
    └── .mvn/
        └── wrapper/
```

---

# 🛠️ Tech Stack

### Backend

* **Java**
* **Spring Boot**
* **Spring Web / WebFlux**
* **Maven**
* **Spring WebClient**
* **Google Gemini API**

### Frontend

* HTML
* CSS
* JavaScript
* Chrome Extension APIs
* Chrome Side Panel API

### Development Tools

* Git / GitHub
* Maven
* Eclipse / Spring Tool Suite or IntelliJ IDEA
* Google Chrome

---

# 🔄 How It Works

The application follows this general flow:

```text
┌───────────────────────┐
│    Chrome Extension   │
│                       │
│    Side Panel UI      │
└───────────┬───────────┘
            │
            │ HTTP Request
            ▼
┌───────────────────────┐
│   Spring Boot API     │
│                       │
│ ResearchController    │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│   ResearchService     │
│                       │
│ Business Logic        │
└───────────┬───────────┘
            │
            │ WebClient
            ▼
┌───────────────────────┐
│     Google Gemini     │
│       AI API          │
└───────────┬───────────┘
            │
            │ AI Response
            ▼
┌───────────────────────┐
│   Spring Boot API     │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│    Chrome Side Panel  │
│                       │
│   Research Result     │
└───────────────────────┘
```

---

# 📁 Backend Structure

## `ResearchAssistantApplication.java`

Main Spring Boot application entry point.

It starts the Spring Boot application and initializes the backend.

---

## `ResearchController.java`

The REST controller responsible for receiving research requests from the Chrome Extension.

The controller acts as the API layer between the extension and the backend service.

```text
Chrome Extension
       ↓
ResearchController
       ↓
ResearchService
```

---

## `ResearchService.java`

Contains the primary research/business logic.

The service communicates with the Gemini API through Spring's `WebClient`.

```text
Research Request
       ↓
ResearchService
       ↓
WebClient
       ↓
Gemini API
       ↓
Gemini Response
```

Keeping this logic inside a service class makes the controller lightweight and easier to maintain.

---

## `ResearchRequest.java`

Represents the request data sent to the research API.

The entity is used to transfer the user's research query from the extension to the Spring Boot application.

---

## `GeminiResponse.java`

Represents the response received from the Gemini API.

It provides a Java representation of the AI response so that the backend can process and return it to the browser extension.

---

## `WebClientConfig.java`

Contains WebClient configuration used for communication with external services.

The project uses WebClient instead of directly making HTTP requests from the controller.

---

# 🧩 Chrome Extension

The `extension-frontend` directory contains the browser extension.

## `manifest.json`

Defines the Chrome Extension configuration, including the extension's permissions and Side Panel configuration.

## `sidepanel.html`

Provides the HTML structure of the research assistant interface.

## `sidepanel.css`

Contains the styling for the Side Panel UI.

## `sidepanel.js`

Contains the client-side JavaScript responsible for interacting with the backend API and updating the research results in the Side Panel.

## `background.js`

Contains the extension background logic and configures the Chrome Side Panel behavior.

---

# ⚙️ Prerequisites

Before running the project, install:

1. **Java JDK**
2. **Maven**
3. **Google Chrome**
4. A **Google Gemini API key**

Verify Java:

```bash
java -version
```

Verify Maven:

```bash
mvn -version
```

---

# 🔑 Gemini API Configuration

The backend requires a Gemini API key.

Open:

```text
ResearchAssistant/src/main/resources/application.properties
```

Configure the Gemini-related properties used by the application.

For example:

```properties
GEMINI_API_KEY=your_api_key_here
```

> Use the exact property names expected by the application's `application.properties` / `ResearchService` configuration.

### ⚠️ Security

Do **not** commit your real API key to GitHub.

Prefer environment variables for production:

```text
GEMINI_API_KEY=your_secret_key
```

and reference the environment variable from Spring configuration.

---

# ▶️ Running the Backend

Go to the backend directory:

```bash
cd ResearchAssistant
```

Run the application using Maven:

```bash
mvn spring-boot:run
```

Alternatively, build the project:

```bash
mvn clean package
```

Then run the generated Spring Boot JAR:

```bash
java -jar target/<generated-jar-name>.jar
```

The backend will start on the port configured in:

```text
src/main/resources/application.properties
```

If no custom port is configured, Spring Boot normally uses:

```text
http://localhost:8080
```

---

# 🧩 Installing the Chrome Extension

The extension does not appear to use a traditional npm-based frontend build system. It consists of the extension files directly.

### Step 1

Open Chrome:

```text
chrome://extensions/
```

### Step 2

Enable:

```text
Developer mode
```

### Step 3

Click:

```text
Load unpacked
```

### Step 4

Select:

```text
extension-frontend
```

directory.

The Research Assistant extension should now appear in your installed extensions.

---

# 🧪 Running the Complete Application

Start the backend first:

```bash
cd ResearchAssistant
mvn spring-boot:run
```

Then load the Chrome extension:

```text
chrome://extensions/
        ↓
Developer mode
        ↓
Load unpacked
        ↓
extension-frontend/
```

After installation:

```text
Chrome
   ↓
Research Assistant Extension
   ↓
Side Panel
   ↓
Enter research query
   ↓
Spring Boot API
   ↓
Gemini API
   ↓
AI response
   ↓
Side Panel
```

---

# 🧪 Testing

The project contains a Spring Boot test class under:

```text
src/test/java/com/research/assistant/
```

Run tests with:

```bash
mvn test
```

For a complete build:

```bash
mvn clean test
```

---

# 🔌 API

The backend exposes a research endpoint through `ResearchController`.

The expected flow is:

```http
POST /<research-endpoint>
Content-Type: application/json
```

Request:

```json
{
  "query": "Your research question"
}
```

The backend processes the query and communicates with Gemini before returning the generated result.

> The exact endpoint path and response structure should be taken from `ResearchController.java` and `GeminiResponse.java` when documenting or integrating against the API.

---

# 🧠 Application Layers

The project follows a basic layered Spring Boot architecture:

```text
Controller Layer
       │
       ▼
Service Layer
       │
       ▼
External AI API
```

### Controller

Handles HTTP requests.

### Service

Contains business logic and Gemini integration.

### Entity / DTO

Represents request and response data.

### Configuration

Provides reusable HTTP client configuration.

This separation makes the application easier to extend and maintain.

---

# 🔐 Security Recommendations

Before deploying this application publicly:

* Never expose the Gemini API key in the Chrome Extension.
* Keep the Gemini API key on the backend.
* Use environment variables or a secret manager.
* Add CORS restrictions for trusted extension origins.
* Add request validation.
* Add rate limiting.
* Add authentication if the API is publicly accessible.
* Avoid logging API keys or sensitive research queries.
* Configure HTTPS for production deployment.

A secure architecture should look like:

```text
Chrome Extension
       │
       │ No Gemini API Key
       ▼
Spring Boot Backend
       │
       │ Secret API Key
       ▼
Gemini API
```

---

# 🚀 Production Deployment

For production, the recommended architecture is:

```text
                   ┌─────────────────┐
                   │ Chrome Extension│
                   └────────┬────────┘
                            │ HTTPS
                            ▼
                   ┌─────────────────┐
                   │ Spring Boot API │
                   │     Server      │
                   └────────┬────────┘
                            │
                            │ HTTPS
                            ▼
                   ┌─────────────────┐
                   │   Gemini API    │
                   └─────────────────┘
```

The backend can be packaged as a JAR:

```bash
mvn clean package
```

and deployed to a Java-compatible cloud/server environment.

---

# 📌 Future Improvements

Possible improvements for the project include:

* [ ] Add user authentication
* [ ] Add research history
* [ ] Save previous queries
* [ ] Add conversation/multi-turn research
* [ ] Add streaming AI responses
* [ ] Add Markdown rendering
* [ ] Add source/citation support
* [ ] Add web search integration
* [ ] Add research summarization
* [ ] Add export to PDF/Markdown
* [ ] Add configurable AI models
* [ ] Add request rate limiting
* [ ] Add centralized error handling
* [ ] Add API documentation with Swagger/OpenAPI
* [ ] Add Docker support
* [ ] Add CI/CD with GitHub Actions
* [ ] Deploy backend to a cloud platform
* [ ] Publish the Chrome Extension

---

# 🐛 Troubleshooting

### Backend does not start

Check:

```bash
java -version
mvn -version
```

Then try:

```bash
mvn clean install
mvn spring-boot:run
```

### Gemini requests fail

Check:

* Gemini API key
* Gemini API availability
* API configuration
* Network connection
* Backend logs

### Chrome Extension cannot communicate with backend

Check:

* Spring Boot backend is running.
* Backend URL configured in the extension is correct.
* CORS configuration allows the extension origin.
* Chrome Extension permissions are correctly configured.

### Extension Side Panel does not open

Check:

```text
chrome://extensions/
```

Then reload the extension and verify that the extension manifest and Side Panel configuration are valid.

---

# 📄 License

Add your preferred license before publishing this project.

For example:

```text
MIT License
```

---

# 👨‍💻 Project

**Research Assistant**

A Java Spring Boot + Chrome Extension based AI research assistant powered by Google Gemini.
