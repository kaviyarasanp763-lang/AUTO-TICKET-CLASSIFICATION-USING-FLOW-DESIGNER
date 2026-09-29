# Auto Ticket Classification using Flow Designer

## Project Overview

**Auto Ticket Classification using Flow Designer** is a ServiceNow project that automates the classification of school IT helpdesk tickets.

The project analyzes keywords in the ticket's Short Description and automatically assigns the appropriate **Category** and **Subcategory** using **ServiceNow Flow Designer**.

## Problem Statement

The school IT helpdesk receives multiple incident requests from students and teachers, including:

- Wi-Fi issues
- Projector failures
- Password problems
- Slow computers

Currently, IT staff manually review each request and assign a category. This project automates that process.

## Objectives

- Automatically classify incidents at the time of creation.
- Reduce manual effort for IT agents.
- Improve ticket routing efficiency.
- Implement a no-code and maintainable solution.
- Send an automated email notification to the caller.
- Store ticket information in a structured format.

## Technologies Used

- ServiceNow
- Flow Designer
- Custom Table
- Choice Fields
- Dependent Choice Fields
- Reference Fields
- Email Notification
- Update Sets

## Project Architecture

```text
Student / Teacher
       |
       v
Create IT Ticket
       |
       v
Short Description
       |
       v
ServiceNow Flow Designer
       |
       +-----------------------+
       |                       |
       v                       v
  Keyword Check          Category Empty?
       |
       v
+-------------------+
| Classification    |
+-------------------+
       |
       +--> WiFi / Network
       |       Category: Network
       |       Subcategory: Wi-Fi
       |
       +--> Projector
       |       Category: Hardware
       |       Subcategory: Projector
       |
       +--> Password / Login
       |       Category: Access
       |       Subcategory: Forgot Password
       |
       +--> Slow / Hanging
       |       Category: Performance
       |       Subcategory: Slow Computer
       |
       v
Update Ticket
       |
       v
Send Email Notification
```

## Custom Table

The project uses a custom table named:

`Incident Workflow`

### Main Fields

| Field | Type |
|---|---|
| Number | Auto Number |
| Caller | Reference |
| Category | Choice |
| Subcategory | Choice |
| Short Description | String |
| Description | String |
| State | Choice |
| Assigned Group | Reference |
| Assigned to | Reference |

## Category and Subcategory

| Category | Subcategory |
|---|---|
| Network | Wi-Fi |
| Hardware | Projector |
| Access | Forgot Password |
| Performance | Slow Computer |

The Subcategory field is dependent on Category.

## Flow Designer Logic

### Trigger

- Trigger: Record Created
- Table: Incident Workflow
- Condition: Category is Empty

### Classification Rules

| Short Description Contains | Category | Subcategory |
|---|---|---|
| Wi-Fi / Network | Network | Wi-Fi |
| Projector | Hardware | Projector |
| Forgot password | Access | Forgot Password |
| Slow Computer | Performance | Slow Computer |

After classification, the flow sends an email notification to the caller.

## Email Notification

The flow sends an email to:

`Caller → Email`

Subject used in the project:

`Your Request for the issue has been submitted.`

## Testing

### Test Scenario 1 — WiFi

Input:

`WiFi not working in library`

Expected result:

- Category → Network
- Subcategory → WiFi
- Email sent to caller

### Test Scenario 2 — Projector

Input:

`Projector not turning on`

Expected result:

- Category → Hardware
- Subcategory → Projector
- Email sent to caller

## Repository Structure

```text
Auto-Ticket-Classification-Flow-Designer/
│
├── README.md
│
├── Documentation/
│   └── Project-Documentation.pdf
│
├── Screenshots/
│   ├── README.txt
│   ├── 01-Update-Set.png
│   ├── 02-Custom-Table.png
│   ├── 03-Fields.png
│   ├── 04-Dependent-Fields.png
│   ├── 05-Flow-Designer.png
│   ├── 06-Trigger.png
│   ├── 07-WiFi-Classification.png
│   ├── 08-Projector-Classification.png
│   ├── 09-Password-Classification.png
│   ├── 10-Slow-Computer-Classification.png
│   ├── 11-Email-Notification.png
│   └── 12-Testing.png
│
├── Update-Set/
│   ├── README.txt
│   └── Project-Update-Set.xml
│
├── .gitignore
└── LICENSE
```

## How to Use This Repository

1. Create a GitHub repository named:
   `Auto-Ticket-Classification-Flow-Designer`
2. Upload all files and folders from this ZIP.
3. Add your ServiceNow screenshots to the `Screenshots` folder.
4. Export the completed ServiceNow Update Set as XML.
5. Put the XML file inside the `Update-Set` folder.
6. Commit the changes to GitHub.

## Future Enhancements

Possible future extensions include:

- Assignment automation
- SLA tracking
- Predictive intelligence

## Author

**Name:** Add your name here

**Project:** Auto Ticket Classification using Flow Designer

**Platform:** ServiceNow
