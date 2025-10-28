# ClaraCore

**HTTP Client for Java Developers**

ClaraCore is a modern, feature-rich HTTP client specifically designed for Java developers. Built with Java Spring Boot backend and React frontend, it provides a seamless experience for API testing, development, and debugging with native Java script execution.

## 🚀 Key Features

### Core Functionality
- **HTTP & REST API Testing** - Support for all standard HTTP methods (GET, POST, PUT, PATCH, DELETE, etc.)
- **Java-Based Scripting** - Write pre-request and test scripts in Java, not JavaScript
- **Environment Management** - Multiple environments with variable substitution using `{{variableName}}` syntax
- **Collections & Folders** - Organize requests hierarchically with nested folders
- **Request History** - Automatic tracking of all API calls with searchable history
- **Global Search** - Fuzzy search across collections, requests, environments, and history

### Advanced Features
- **AI Assistant (Embabel-Powered)** - Five specialized AI agents for API testing, debugging, performance analysis, security scanning, and documentation generation
- **Built-in Mock Server** - Create mock endpoints with custom responses for testing
- **Google Cloud Pub/Sub** - Native support for Pub/Sub topics and subscriptions
- **Collection Runner** - Execute entire collections or folders with environment-specific variables
- **Code Generation** - Generate ready-to-use Java code snippets from requests
- **Postman Compatibility** - Import/export Postman collections and environments
- **Proxy Support** - HTTP, SOCKS4, and SOCKS5 proxies with authentication (including Tor/.onion sites)

### Developer Experience
- **Tab-Based Interface** - Work on multiple requests simultaneously
- **Syntax Highlighting** - Code editor with Java, JSON, XML syntax highlighting
- **Request Templates** - Quick-start templates for common request patterns
- **Keyboard Shortcuts** - Efficient keyboard-driven workflow
- **Dark/Light Theme** - Comfortable UI for extended coding sessions

## 📦 Installation

### Download
Download the latest release from the [Releases page](https://github.com/cristigirbovan/claracore/releases):
- **Windows**: `ClaraCore-1.0.0-portable.exe`

### System Requirements
- **Operating System**: Windows 10+
- **Java Runtime**: JDK 17 or higher (embedded in the application)
- **Memory**: 2GB RAM minimum, 4GB recommended
- **Disk Space**: 200MB for installation

### First Launch
1. Extract the application
2. Launch ClaraCore
3. The Java sidecar will start automatically on first run
4. You're ready to make your first request!

## 🎯 Quick Start

### Making Your First Request

1. **Create a Collection**
   - Click "New Collection" in the sidebar
   - Give it a name (e.g., "My API Tests")

2. **Add a Request**
   - Right-click the collection → "New Request"
   - Enter request details:
     - **Method**: GET
     - **URL**: `https://httpbin.org/get`
   - Click "Send"

3. **View Response**
   - See status code, response time, and body
   - Explore headers and response data

### Working with Environments

Environments allow you to manage different configurations (dev, staging, production).

**Create an Environment:**
1. Go to the **Environments** tab in the sidebar
2. Click "New Environment"
3. Add variables:
   - Key: `baseUrl`
   - Value: `https://api.example.com`
4. Click on the environment to activate it

**Use Variables in Requests:**
```
{{baseUrl}}/users
{{baseUrl}}/orders/{{orderId}}
```

Variables can be used in:
- URLs
- Headers
- Query parameters
- Request body
- Authentication credentials

### Pre-Request Scripts (Java)

Execute Java code before sending the request:

```java
import java.time.Instant;

// Set timestamp header
String timestamp = String.valueOf(Instant.now().toEpochMilli());
pm.environment.set("timestamp", timestamp);

// Generate random ID
String requestId = java.util.UUID.randomUUID().toString();
pm.request.addHeader("X-Request-ID", requestId);

System.out.println("Request ID: " + requestId);
```

**Available Objects:**
- `pm.environment` - Get/set environment variables
- `pm.request` - Modify request (headers, body, params)
- `pm.variables` - Access collection variables
- `System.out` - Console logging

### Test Scripts (Java)

Write assertions to validate responses:

```java
import static org.junit.jupiter.api.Assertions.*;

// Test status code
assertEquals(200, pm.response.code(), "Status should be 200");

// Parse JSON response
com.fasterxml.jackson.databind.JsonNode json = pm.response.json();
assertTrue(json.has("data"), "Response should have data field");

// Test response time
assertTrue(pm.response.responseTime() < 1000, "Response time should be under 1s");

// Test headers
String contentType = pm.response.header("Content-Type");
assertTrue(contentType.contains("application/json"), "Content-Type should be JSON");

System.out.println("All tests passed!");
```

## 🔧 Core Features

### AI Assistant (Embabel Integration)

ClaraCore includes an AI-powered assistant built on [Embabel](https://github.com/embabel) - an awesome and fun agent framework that makes building intelligent agents a joy! Five specialized agents are available:

**Available Agents:**
- **API Testing Agent** - Generates comprehensive AI-powered tests for endpoints
- **API Debug Agent** - Diagnoses errors and provides actionable fix recommendations
- **Performance Analysis Agent** - Analyzes endpoint performance and suggests optimizations
- **Security Scan Agent** - Identifies vulnerabilities and provides remediation guidance
- **Documentation Generator Agent** - Creates comprehensive API documentation automatically

**Configuration:**
1. Open Settings → AI
2. Configure your AI model and API key (supports Anthropic Claude and OpenAI-compatible endpoints)
3. Click "Ask AI" in any request to get intelligent assistance

**Use Cases:**
- Automatic test case generation
- Debugging complex API errors
- Performance bottleneck identification
- Security vulnerability scanning
- API documentation creation

### Proxy Support

Route requests through proxy servers for enterprise environments, VPNs, and anonymity networks:

**Supported Proxy Types:**
- **HTTP Proxy** - Standard HTTP proxy with Basic authentication
- **SOCKS4** - Legacy SOCKS protocol
- **SOCKS5** - Modern SOCKS protocol (recommended for Tor, VPN, corporate proxies)

**Configuration:**
1. Open Settings → Network
2. Enable "Enable Proxy"
3. Select proxy type and enter server (e.g., `localhost:9050` for Tor)
4. Add authentication credentials if required

**Tor & .onion Sites:**
To access .onion sites:
1. Install and run Tor Browser (starts Tor service on localhost:9050)
2. Configure ClaraCore: SOCKS5 proxy → `localhost:9050`
3. Make requests to .onion addresses

**Common Use Cases:**
- Corporate firewall bypass
- SSH tunneling: `ssh -D 1080 user@server`
- Tor anonymity network access
- VPN proxy endpoints
- Development environment routing

### Collections & Organization

**Collections** are containers for related requests. They support:
- Nested folders (unlimited depth)
- Request templates
- Collection-level variables
- Drag-and-drop reordering
- Bulk operations (run, export, delete)

**Right-click menu options:**
- New Request
- New Folder
- Rename
- Duplicate
- Delete
- Run Collection

### Mock Server

Create mock endpoints for testing without backend dependencies:

1. Go to **Mocks** tab
2. Click "Create Mock Endpoint"
3. Configure:
   - **Path**: `/api/users`
   - **Method**: GET
   - **Status Code**: 200
   - **Response Body**:
   ```json
   {
     "users": [
       {"id": 1, "name": "John Doe"},
       {"id": 2, "name": "Jane Smith"}
     ]
   }
   ```
4. Click "Start Server"
5. Mock server runs on `http://localhost:47823/api/mock`

**Use cases:**
- Frontend development without backend
- Testing error scenarios
- API contract validation
- Integration testing

### Google Cloud Pub/Sub

Native support for Google Cloud Pub/Sub operations:

**Create Topic:**
```
Project ID: my-project
Topic ID: user-events
```

**Publish Message:**
```json
{
  "userId": "12345",
  "event": "user.created",
  "timestamp": "2025-01-26T12:00:00Z"
}
```

**Pull Messages:**
```
Subscription ID: user-events-sub
Max Messages: 10
```

**Emulator Support:**
Set `PUBSUB_EMULATOR_HOST=localhost:8085` for local testing.

### Code Generation

Generate production-ready Java code from any request:

1. Configure your request completely
2. Click "Code" button in request panel
3. Select template:
   - **Java WebClient** (modern, async)
   - **OkHttp** (popular HTTP client)
   - **Spring RestTemplate** (Spring Boot)
   - **Apache HttpClient** (legacy support)
4. Copy generated code

**Example Output (Java 11 HttpClient):**
```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.example.com/users"))
    .header("Authorization", "Bearer token123")
    .GET()
    .build();

HttpResponse<String> response = client.send(request,
    HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

### Import/Export

**Import from Postman:**
1. File → Import → Select Collection/Environment file
2. Choose Postman JSON format
3. Import with full structure (folders, requests, variables)

**Note:** JavaScript scripts in Postman collections are converted to Java with comments showing original code. Complex scripts may need manual adjustment.

**Export to Postman:**
1. Right-click collection → Export
2. Select Postman v2.1 format
3. File is compatible with Postman, Newman CLI, and other tools

**Formats Supported:**
- Postman Collection v2.1
- Postman Environment JSON
- ClaraCore native format

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl/Cmd + N` | New Request |
| `Ctrl/Cmd + S` | Save Request |
| `Ctrl/Cmd + Enter` | Send Request |
| `Ctrl/Cmd + K` | Global Search |
| `Ctrl/Cmd + Shift + O` | Import Collection |
| `Ctrl/Cmd + Shift + E` | Export Collection |
| `Ctrl/Cmd + ,` | Open Settings |
| `Ctrl/Cmd + /` | Show Shortcuts |
| `Ctrl/Cmd + W` | Close Tab |
| `Ctrl/Cmd + T` | Duplicate Tab |
| `Esc` | Close Modal/Dialog |

## 📚 Advanced Usage

### Collection Runner

Execute entire collections or folders with configurable iterations:

1. Right-click collection/folder → "Run Collection"
2. Configure:
   - **Environment**: Select active environment
   - **Iterations**: Number of times to run (1-1000)
   - **Delay**: Delay between requests (ms)
   - **Continue on Error**: Keep running if request fails
3. Click "Run"
4. View results with pass/fail status

**Use Cases:**
- Integration testing
- Load testing (with iterations)
- Smoke tests after deployment
- Data seeding

### Dynamic Variables

ClaraCore supports dynamic variables that generate values automatically:

- `$timestamp` - Current Unix timestamp (seconds)
- `$timestampMillis` - Current timestamp (milliseconds)
- `$randomInt` - Random integer (0-1000)
- `$randomUUID` - Random UUID v4
- `$randomString` - Random alphanumeric string (10 chars)

**Example:**
```
URL: {{baseUrl}}/users?timestamp=$timestamp
Header: X-Request-ID: $randomUUID
Body: {"orderId": "$randomString"}
```

### Request Settings

Configure request-specific behavior:

- **Timeout**: Request timeout in milliseconds (default: 30000)
- **Follow Redirects**: Automatically follow HTTP redirects (default: true)
- **Max Redirects**: Maximum redirect hops (default: 5)
- **Validate SSL**: Verify SSL certificates (default: true)
- **Max Response Size**: Limit response body size (default: 256KB)

### Authentication

Supported authentication methods:

**Bearer Token:**
```
Token: {{accessToken}}
```

**Basic Auth:**
```
Username: user@example.com
Password: {{password}}
```

**API Key:**
```
Key: X-API-Key
Value: {{apiKey}}
Location: Header or Query Parameter
```

**OAuth 2.0:**
```
Access Token: {{oauth_token}}
Token Type: Bearer
```

## 🛠️ Configuration

### Java Sidecar

ClaraCore uses a Java Spring Boot sidecar for HTTP operations:

- **Port**: 47823 (auto-assigned)
- **Health Check**: Automatic on startup
- **Logs**: Available in Help → View Logs
- **Restart**: Help → Restart Java Sidecar

### Settings

Access via `Ctrl/Cmd + ,`:

**General:**
- Theme (Light/Dark/System)
- Request timeout
- Auto-save interval
- History limit

**Editor:**
- Font size
- Tab size
- Line wrapping
- Auto-format JSON/XML

**Network:**
- Proxy settings (HTTP, SOCKS4, SOCKS5)
- Proxy authentication (username/password)
- SSL certificate validation
- Custom CA certificates

**AI:**
- AI model selection (Claude, GPT, custom endpoints)
- API key configuration
- Agent behavior customization

## 🤝 Support & Community

### Getting Help

- **Issues**: [GitHub Issues](https://github.com/cristigirbovan/claracore/issues)
- **Email**: cristi.girbovan@gmail.com

### Reporting Bugs

When reporting issues, please include:
1. ClaraCore version (Help → About)
2. Operating system and version
3. Steps to reproduce
4. Expected vs actual behavior
5. Screenshots if applicable
6. Console logs (Help → View Logs)

### Feature Requests

We welcome feature requests! Please:
1. Check existing issues first
2. Describe the use case
3. Explain expected behavior
4. Provide examples if applicable

## 📄 License

ClaraCore is open source software licensed under the **Apache License 2.0**.

**What this means:**
- ✅ Free to use for any purpose (personal, commercial, enterprise)
- ✅ Free to modify and distribute
- ✅ Patent protection included
- ✅ Can be used in proprietary software
- ✅ No restrictions on commercial use

See the [LICENSE](LICENSE) file for full details.

## 🙏 Acknowledgments

ClaraCore is powered by [Embabel](https://github.com/embabel), an awesome and fun agent framework that makes building intelligent AI agents a joy! The five specialized agents in ClaraCore (API Testing, Debugging, Performance Analysis, Security Scanning, and Documentation Generation) are built on Embabel's powerful GOAP (Goal-Oriented Action Planning) runtime.

If you're interested in building AI agents, check out Embabel - it's a great framework to work with!

© 2025 ClaraCore. Licensed under Apache 2.0.
