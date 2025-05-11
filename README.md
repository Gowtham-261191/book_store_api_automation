📚 Bookstore API Automation Project
Automated E2E testing for Bookstore APIs using TestNG, Rest Assured, and Java 17 with full CI/CD support and Allure reporting.

🚀 Project Overview
This repository automates the key API flows of a Bookstore service. It uses a Test-Driven Development (TDD) approach with TestNG + Rest Assured to enable scalable, CI-ready test suites.

🧰 Stack in Use
Area	Tool/Framework
Language	Java 17
API Testing	Rest Assured
Test Runner	TestNG (Retry, Parallel, Listeners)
Build Tool	Maven
Reporting	Allure
IDE	IntelliJ IDEA

🎯 Key API Endpoints Tested
http

POST    /signup         → Register a new user  
POST    /login          → Login & get authentication token  
POST    /books          → Add a new book  
PUT     /books/{id}     → Update book info  
GET     /books/{id}     → Get book by ID  
GET     /books          → Get list of all books  
DELETE  /books/{id}     → Delete a book by ID  
📋 Setup Guide
🔧 Prerequisites
Java 17 or later

Maven 3.6+

IntelliJ IDEA (or any IDE with Maven support)

🛠 Installation

# Clone the repo
git clone [https://github.com/Gowthaman-261191/book-store-api-automation.git](https://github.com/Gowtham-261191/book_store_api_automation.git)
cd book-store-api-automation

# Build and test
mvn clean test
Environment config files available under /resources:

application-STAGE.properties

application-QA.properties

You can set environment-specific base URL and ports here.

✅ Test Execution
Run all tests:

mvn test
Switch environments using a profile or configuration override.

📊 Allure Reports
After execution:

mvn allure:report
Serve the report locally:


allure serve target/allure-results
Allure displays test categories, trends, and clear failure reasons (assertion vs server errors).

🔄 CI/CD Workflow: Jenkins + Ngrok
Jenkins Configuration
Install plugins:

Git

GitHub Integration

Maven

Allure

Pipeline

Run Jenkins locally:

jenkins
Use Ngrok to expose local server for GitHub webhook:

ngrok http http://localhost:8080
Copy the forwarded URL.

Dev Repo Jenkinsfile
groovy

pipeline {
  agent any
  stages {
    stage('Build Dev') {
      steps {
        echo 'Build or test dev code here'
      }
    }
    stage('Trigger QA Automation') {
      steps {
        build job: 'QA-Repo'
      }
    }
  }
}
QA Repo Jenkinsfile
groovy
pipeline {
  agent any
  tools {
    maven 'Maven 3.6.3'
    allure 'Allure'
  }
  stages {
    stage('Checkout') {
      steps {
        git url: '<gitUrl>', branch: '<BranchName>'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'mvn clean test'
      }
    }
    stage('Generate Allure Report') {
      steps {
        sh 'mvn allure:report'
      }
    }
  }
  post {
    always {
      allure([
        includeProperties: false,
        results: [[path: 'target/allure-results']]
      ])
    }
  }
}
🌐 Webhook Setup (GitHub → Jenkins)
Go to GitHub > Repo > Settings > Webhooks
Set the payload URL using the format:

https://<user>:<token>@<ngrok-url>/job/DevRepo/build
✅ This triggers the Dev Job which in turn runs QA automation and generates an Allure Report.

🧪 CI/CD Summary
Trigger	Action
Commit to Dev	Jenkins builds Dev project
→ QA automation job is triggered
→ Allure report is generated automatically

