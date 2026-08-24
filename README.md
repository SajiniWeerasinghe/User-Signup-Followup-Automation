# User-Signup-Followup-Automation
An automated user signup and follow-up workflow built with n8n.

An automated **user signup and follow-up workflow** built with **n8n**. The workflow receives new registration data through a webhook, sends a personalized welcome email, checks the user's role, and automatically stores Guest users in a dedicated Google Sheet.

This project demonstrates how **Google Forms, Google Apps Script, n8n, SMTP, and Google Sheets** can be connected to automate a user registration and follow-up process.

##  Workflow

![Workflow](screenshots/workflow.png)

```text
Google Form
     │
     ▼
Google Apps Script
     │
     ▼
n8n Webhook
     │
     ▼
Send Welcome Email
     │
     ▼
Check User Role
     │
     ├───────────────┐
     │               │
   Guest            Other
     │               │
     ▼               ▼
Google Sheets       End
     │
     ▼
Store Guest User
```

##  Features

* 📩 Receives registration data through an n8n Webhook
* 👋 Sends a personalized welcome email automatically
* 🔀 Checks the registered user's role
* 📊 Stores Guest users in a dedicated Google Sheet
* ⚡ Runs automatically after each form submission
* 🔗 Integrates multiple services into one automated workflow
* 🧩 Uses conditional logic to control the workflow

## 🛠️ Technologies Used

| Technology             | Purpose                            |
| ---------------------- | ---------------------------------- |
| **n8n**                | Workflow automation                |
| **Google Forms**       | Collects user registration data    |
| **Google Apps Script** | Sends form data to the n8n webhook |
| **SMTP**               | Sends personalized welcome emails  |
| **Google Sheets**      | Stores Guest user information      |

## 📋 How It Works

### 1. User submits the registration form

A user completes the Google Form with registration details including:

* First Name
* Last Name
* Email
* Phone Number
* Role

### 2. Google Apps Script sends the data

Google Apps Script collects the submitted form data and sends it to the n8n Webhook as a JSON request.

### 3. n8n receives the submission

The **Webhook** node receives the registration data and passes it to the email automation.

### 4. Welcome email is sent

The **Send Welcome Email** node automatically sends a personalized welcome email to the registered user's email address.

The user's first name is dynamically inserted into the email.

Example:

```text
Subject: Welcome to Our Community!

Hello Sajini,

Welcome to our community! We're excited to have you with us.

Thank you for signing up. We hope you enjoy being part of our community and look forward to having you with us.

Best regards,
The Community Team
```

### 5. User role is checked

The **IF** node checks whether the user's role is:

```text
Guest
```

If the role is `Guest`, the workflow continues to Google Sheets.

If the role is not `Guest`, the workflow ends.

### 6. Guest user is stored

Guest users are automatically added to a dedicated Google Sheet.

The following information is stored:

| Field        | Description          |
| ------------ | -------------------- |
| First Name   | User's first name    |
| Last Name    | User's last name     |
| Email        | User's email address |
| Phone Number | User's phone number  |
| Role         | User's role          |


## 🔧 Setup

### Prerequisites

You will need:

* An n8n account or self-hosted n8n instance
* A Google Form
* A Google Apps Script project
* A Google account
* A Google Sheet
* An SMTP-enabled email account

### 1. Download or clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/n8n-user-signup-automation.git
```

```bash
cd n8n-user-signup-automation
```

### 2. Import the workflow

1. Open your n8n workspace.
2. Open the workflow editor.
3. Select the workflow menu.
4. Choose **Import from File**.
5. Select:

```text
workflow/user-signup-followup-automation.json
```

n8n supports importing workflow JSON files directly from the editor.

### 3. Configure credentials

After importing the workflow, configure your own credentials for:

* SMTP
* Google Sheets

The GitHub version intentionally does not contain private credentials.

### 4. Configure Google Sheets

Replace:

```text
YOUR_GOOGLE_SHEET_ID
```

with your own Google Sheet ID inside n8n.

Create a sheet with the following columns:

```text
First Name | Last Name | Email | Phone number | Role
```

### 5. Configure the email sender

Replace:

```text
YOUR_EMAIL@example.com
```

with your own email address in the **Send Welcome Email** node.

Then select your configured SMTP credential.

### 6. Configure Google Apps Script

Configure Google Apps Script to send the Google Form response to the n8n webhook using a `POST` request.

Example JSON payload:

```json
{
  "First Name": "Sajini",
  "Last Name": "Weerasinghe",
  "Email": "user@example.com",
  "Phone number": "+94XXXXXXXXX",
  "Role": "Guest"
}
```

Make sure the field names match the expressions used in the n8n workflow.

## 🔐 Security

This repository intentionally does **not** contain:

* SMTP passwords
* Google credentials
* API keys
* Private Google Sheet URLs
* Personal user information
* n8n credential IDs
* Private webhook configuration
* n8n instance information

Always configure credentials directly inside your own n8n instance.

 
 
 
