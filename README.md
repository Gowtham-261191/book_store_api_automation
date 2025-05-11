# 📚 Bookstore API Automation Project
Automated E2E testing for Bookstore APIs using Java 17, Rest Assured, and TestNG, complete with CI/CD integration and Allure reporting.

🚀 Project Overview
This repository automates critical API workflows of a Bookstore service using a Test-Driven Development (TDD) approach. Built with TestNG + Rest Assured, the framework supports scalable, maintainable, and CI-ready test suites.

| Area        | Tool/Framework                                         |
| ----------- | ------------------------------------------------------ |
| Language    | Java 17                                                |
| API Testing | Rest Assured                                           |
| Test Runner | TestNG (Retry analyzer, Parallel execution, Listeners) |
| Build Tool  | Maven                                                  |
| Reporting   | Allure                                                 |
| IDE         | IntelliJ IDEA                                          |

| Method | Endpoint      | Description                |
| ------ | ------------- | -------------------------- |
| POST   | `/books`      | Add a new book             |
| PUT    | `/books/{id}` | Update book information    |
| GET    | `/books/{id}` | Retrieve book by ID        |
| GET    | `/books`      | Retrieve all books         |
| DELETE | `/books/{id}` | Delete a book by ID        |



📋 Setup Guide
🔧 Prerequisites
Java 17+

Maven 3.6+

IntelliJ IDEA (or any IDE with Maven support)

# Clone the repo
git clone https://github.com/Gowthaman-261191/book-store-api-automation.git
cd book-store-api-automation

# Build and test
mvn clean test

# 📊 Allure Report Integration
Generate Allure Report: mvn allure:report

Serve Locally: allure serve target/allure-results

# Benefits:

📌 Test case categorization

📉 Trends and history

❌ Differentiates product vs. test script failures


# 🔄 CI/CD Workflow (Jenkins + Ngrok)
## ✅ Jenkins Setup
Install the following Jenkins plugins:

Git

GitHub

Maven Integration

Pipeline

Allure

# 🧪 Dev Repo Jenkinsfile

pipeline {agent anystages {stage('Build Dev') {steps {echo 'Build or test dev code here'}}stage('Trigger QA Automation') {steps {build job: 'QA-Repo'}}}}

# 🧪 QA Repo Jenkinsfile

pipeline {agent anytools {maven 'Maven 3.6.3'allure 'Allure'}stages {stage('Checkout') {steps {git url: '<gitUrl>', branch: '<BranchName>'}}stage('Build and Test') {steps {sh 'mvn clean test'}}
    stage('Generate Allure Report') {steps {sh 'mvn allure:report'}}}post {always {allure([includeProperties: false,results: [[path: 'target/allure-results']]])}}}

# 🌐 GitHub Webhook Setup
Go to GitHub > Your Repo > Settings > Webhooks

Add a new webhook with the following payload URL format:
https://<user>:<token>@<ngrok-url>/job/DevRepo/build

✅ This triggers the Dev Jenkins job, which in turn executes QA automation and generates the Allure report.

# 🔁 CI/CD Summary
| Action        | Result                                   |
| ------------- | ---------------------------------------- |
| Commit to Dev | Jenkins builds Dev project               |
|               | → Triggers QA automation job             |
|               | → Allure report generated in QA pipeline |




