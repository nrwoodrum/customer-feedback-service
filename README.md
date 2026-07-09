# Feedback Service

A Spring Boot application that processes and analyzes customer feedback using AI-powered insights from Google's Gemini API. The service reads feedback data, performs sentiment analysis, and provides both web dashboard and REST API interfaces for accessing feedback information.

## Features

- **AI-Powered Analysis**: Integrates with Google Gemini API for intelligent feedback analysis
- **Sentiment Analysis**: Processes feedback to extract sentiment information
- **Dashboard UI**: Web-based dashboard to visualize feedback summaries
- **REST API**: JSON endpoints for programmatic access to feedback data
- **Data Parsing**: Parses and structures raw feedback data with metadata
- **Caching**: Implements caching for improved performance

## Prerequisites

- **Java 21 or higher**
- **Maven 3.6+**
- **Google Gemini API Key** - Obtain from [Google AI Studio](https://ai.google.dev/)
- **Git** (for version control)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/nrwoodrum/customer-feedback-service.git
cd feedback-service
```

### 2. Verify Java Installation

```bash
java -version
```

Ensure you have Java 21 or higher installed.

## Configuration

### Set Up Environment Variables

The application requires a Gemini API key. Set it as an environment variable:

**Linux/macOS:**
```bash
export GEMINI_API_KEY="your-api-key-here"
```

**Windows (Command Prompt):**
```cmd
set GEMINI_API_KEY=your-api-key-here
```

**Windows (PowerShell):**
```powershell
$env:GEMINI_API_KEY="your-api-key-here"
```

### Application Properties

The application runs on port **8080** by default. To change this, modify [src/main/resources/application.properties](src/main/resources/application.properties):

```properties
server.port=8080
```

## Running the Application

### Option 1: Using Maven (Recommended)

From the project root directory:

```bash
./mvnw spring-boot:run
```

On Windows:
```cmd
mvnw.cmd spring-boot:run
```

### Option 2: Build and Run as JAR

```bash
./mvnw clean package
java -Dgemini.api-key=$GEMINI_API_KEY -jar target/feedback-service-0.0.1-SNAPSHOT.jar
```

The application will start and be accessible at `http://localhost:8080`

## API Endpoints

### Dashboard
- **GET** `/` - Displays the web dashboard with feedback summary visualization

### Feedback Data
- **GET** `/getfeedback` - Returns all feedback entries in JSON format
  ```json
  [
    {
      "id": 1,
      "customer": "John Doe",
      "department": "Retail",
      "date": "2024-01-15",
      "comment": "Great service!",
      "sentiment": "positive",
      "enhancement": "AI-generated insights about the feedback"
    }
  ]
  ```

## Project Structure

```
feedback-service/
├── src/
│   ├── main/
│   │   ├── java/com/retailstore/feedback/
│   │   │   ├── controller/
│   │   │   │   └── FeedbackController.java       # REST endpoints and web routes
│   │   │   ├── service/
│   │   │   │   ├── FeedbackService.java          # Feedback processing logic
│   │   │   │   └── GeminiService.java            # Gemini API integration
│   │   │   ├── model/
│   │   │   │   ├── FeedbackEntry.java            # Raw feedback data model
│   │   │   │   ├── EnhancedFeedback.java         # AI-enriched feedback model
│   │   │   │   └── FeedbackSummary.java          # Summary statistics model
│   │   │   └── FeedbackServiceApplication.java   # Application entry point
│   │   └── resources/
│   │       ├── application.properties             # Configuration
│   │       └── templates/
│   │           ├── dashboard.html                 # Dashboard UI
│   │           └── error.html                     # Error page
│   └── test/
│       └── java/...                               # Unit tests
├── pom.xml                                        # Maven dependencies
├── mvnw / mvnw.cmd                               # Maven wrapper
└── README.md                                      # This file
```

## Technologies Used

- **Spring Boot 3.2.3** - Web framework
- **Java 21** - Programming language
- **Thymeleaf** - Server-side templating
- **OkHttp 4.12.0** - HTTP client for API calls
- **Jackson** - JSON processing
- **Spring Boot DevTools** - Development utilities
- **Maven** - Build tool

## Building the Project

### Clean Build
```bash
./mvnw clean build
```

### Run Tests
```bash
./mvnw test
```

### Create JAR Package
```bash
./mvnw package
```

## Development

### Hot Reload
The project includes Spring Boot DevTools, which enables hot reload during development:

```bash
./mvnw spring-boot:run
```

Changes to Java files or templates will automatically reload without manual restart.

### Logging
Debug logging is enabled for the `com.retailstore` package. Check console output for detailed logs:

```
DEBUG com.retailstore.feedback - Detailed operation logs
INFO org.springframework.web - Spring Web framework logs
```

## Data Files

The application expects feedback data in:
- `sentiment_feedback_output.txt` - Processed feedback with sentiment analysis
- `sentiment_feedback_output_encoded.txt` - Encoded version of feedback data

## Error Handling

The application provides user-friendly error pages and responses:
- Dashboard errors are displayed on the error page
- API errors return appropriate HTTP status codes with error details

## Security Considerations

⚠️ **Important:**
- Never commit your Gemini API key to version control
- Always use environment variables for sensitive credentials
- Consider using `.env` files with a tool like `dotenv` in development
- The `.gitignore` file should exclude sensitive files

## License

This project is provided as-is for educational and learning purposes.

## Support

For issues or questions:
1. Check the [Spring Boot documentation](https://spring.io/projects/spring-boot)
2. Review [Gemini API documentation](https://ai.google.dev/docs)
3. Check application logs for detailed error messages

## Next Steps

- [ ] Deploy to production environment
- [ ] Set up database for persistent feedback storage
- [ ] Implement user authentication
- [ ] Add more sophisticated analytics
- [ ] Create batch feedback processing capabilities
- [ ] Set up monitoring and alerting

---

**Last Updated:** July 9, 2026