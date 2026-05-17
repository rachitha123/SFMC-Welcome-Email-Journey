# Salesforce Marketing Cloud – Welcome Email Journey

## Project Overview

This is a practice project built to demonstrate foundational knowledge of **Salesforce Marketing Cloud (SFMC)**, specifically Journey Builder, Data Extensions, and email personalisation using AMPscript.

The project simulates a **2-step Welcome Email Journey** for new subscribers of a fictional healthcare platform called *MediConnect*. It covers the full journey lifecycle: subscriber entry, segmentation, email delivery, and a follow-up touchpoint.

---

## Tools & Features Used

| SFMC Feature | Purpose |
|---|---|
| Journey Builder | Designing the 2-step automated welcome flow |
| Data Extension | Storing subscriber data with custom fields |
| AMPscript | Personalising email content (first name, preference) |
| Entry Source | Triggering the journey from a form submission event |
| Wait Activity | Adding a 3-day delay between Email 1 and Email 2 |
| Goal Setting | Tracking profile completion as the journey success metric |

---

## Journey Structure

```
[New Subscriber Signs Up]
        |
        v
  [Journey Entry]
  Entry Source: Form Submit Event
        |
        v
  [Email 1 – Welcome Email]
  Subject: "Welcome to MediConnect, %%FirstName%%!"
  Sent: Immediately on entry
        |
        v
  [Wait Activity – 3 Days]
        |
        v
  [Email 2 – Getting Started Guide]
  Subject: "Here's how to get the most out of MediConnect"
  Sent: Day 3 after entry
        |
        v
  [Journey Exit]
```

---

## Subscriber Data Extension Fields

| Field Name | Data Type | Required | Description |
|---|---|---|---|
| SubscriberKey | Text (50) | Yes | Unique ID for each subscriber |
| FirstName | Text (50) | Yes | Used for AMPscript personalisation |
| LastName | Text (50) | No | Full name for records |
| EmailAddress | Email Address | Yes | Primary send address |
| SignupDate | Date | Yes | Used for journey entry trigger |
| Preference | Text (50) | No | Content preference (General / Specialist) |
| ProfileComplete | Boolean | No | Journey goal metric |

---

## Sample Data

See [`subscriber-data-sample.csv`](./subscriber-data-sample.csv) for a sample of 10 fictional subscriber records matching the Data Extension structure above.

---

## Email Templates

See [`welcome-email-template.html`](./welcome-email-template.html) for the HTML email template used in Email 1, including AMPscript personalisation blocks.

---

## Journey Flow Logic

See [`journey-flow-logic.md`](./journey-flow-logic.md) for the full decision logic, entry criteria, wait conditions, and exit rules documented step by step.

---

## Key Learnings

- Understood how **Data Extensions** differ from standard contact lists and why they are used in SFMC
- Learned how **Journey Builder Entry Sources** work (API Event vs Form Submit vs Data Extension entry)
- Practiced writing basic **AMPscript** to personalise subject lines and email body content
- Understood the role of **Wait Activities** in spacing out communications to avoid overwhelming subscribers
- Learned how to define **Journey Goals** to measure success (e.g. ProfileComplete = True)

---

## About This Project

This is a documentation and simulation project built as part of self-directed learning on the **Salesforce Marketing Cloud Email Specialist** course (Udemy). All subscriber data is fictional. No live SFMC org was used.

**Tools used for documentation:** Markdown, HTML, CSV  
**Certification in progress:** Salesforce Marketing Cloud Email Specialist
