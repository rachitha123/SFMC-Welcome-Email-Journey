# Journey Flow Logic – Welcome Email Journey

## Journey Overview

**Journey Name:** MediConnect Welcome Journey  
**Platform:** Salesforce Marketing Cloud – Journey Builder  
**Goal:** Guide new subscribers through a 2-email welcome sequence and encourage them to complete their profile  
**Success Metric:** ProfileComplete = TRUE  

---

## Entry Configuration

| Setting | Value |
|---|---|
| Entry Source | Form Submit API Event |
| Trigger | New subscriber completes signup form on MediConnect website |
| Entry Criteria | EmailAddress is not null AND SignupDate = Today |
| Re-entry | Not allowed (each subscriber enters only once) |
| Injection Method | Real-time (subscriber enters as soon as form is submitted) |

---

## Step-by-Step Journey Logic

### Step 1 – Journey Entry
- Subscriber submits the MediConnect signup form
- SFMC receives the API event with subscriber data
- Record is added to the **MediConnect_Subscribers** Data Extension
- Subscriber enters the journey immediately

---

### Step 2 – Email 1: Welcome Email
**Send Time:** Immediately on entry  
**From Name:** MediConnect Team  
**From Email:** hello@mediconnect.com  
**Subject Line:** Welcome to MediConnect, %%FirstName%%!  
**Preview Text:** You're all set. Here's what happens next.

**Email Content Summary:**
- Personalised greeting using AMPscript (%%FirstName%%)
- Brief introduction to MediConnect
- Single CTA button: "Complete Your Profile"
- Dynamic content block: shows General or Specialist content based on Preference field

**AMPscript Used:**
```
%%[ VAR @firstName SET @firstName = AttributeValue("FirstName") ]%%
Hello %%=v(@firstName)=%%,
```

---

### Step 3 – Wait Activity
**Duration:** 3 days  
**Type:** Duration Wait (not a specific date)  
**Purpose:** Give the subscriber time to read Email 1 and take action before sending Email 2  

---

### Step 4 – Email 2: Getting Started Guide
**Send Time:** 3 days after Email 1  
**From Name:** MediConnect Team  
**From Email:** hello@mediconnect.com  
**Subject Line:** Here's how to get the most out of MediConnect, %%FirstName%%  
**Preview Text:** Tips, features, and your next steps inside.

**Email Content Summary:**
- Personalised greeting
- 3 tips for using the MediConnect platform
- Reminder CTA: "Complete Your Profile" (for subscribers who haven't yet)
- Link to Help Centre

---

### Step 5 – Journey Exit
- Subscriber exits the journey after Email 2 is sent
- If ProfileComplete = TRUE at any point, subscriber also exits via the Journey Goal
- No further emails are sent from this journey

---

## Journey Goal

| Setting | Value |
|---|---|
| Goal Name | Profile Completed |
| Goal Criteria | ProfileComplete = TRUE |
| Goal Evaluation | Checked at each step |
| Outcome | If goal is met before Email 2, subscriber exits early (goal achieved) |

---

## Suppression & Exit Rules

| Rule | Detail |
|---|---|
| Unsubscribe | Subscriber is removed immediately if they unsubscribe at any point |
| Bounce | Hard bounces trigger automatic exit and suppress future sends |
| Re-entry | Disabled — subscriber can only go through this journey once |

---

## Segmentation Logic (Dynamic Content in Email 1)

The first email uses a content block that changes based on the subscriber's **Preference** field:

```
%%[ IF @preference == "Specialist" THEN ]%%
  <!-- Show Specialist-focused content block -->
%%[ ELSE ]%%
  <!-- Show General audience content block -->
%%[ ENDIF ]%%
```

| Segment | Preference Value | Content Shown |
|---|---|---|
| General Audience | General | Overview of all MediConnect features |
| Healthcare Specialists | Specialist | Specialist tools and clinical resource links |

---

## Notes

- This journey was designed as a practice simulation based on SFMC Journey Builder training
- No live SFMC instance was used — logic is documented for learning and portfolio purposes
- Data Extension structure is defined in README.md
- Sample subscriber data is in subscriber-data-sample.csv
