# Root Cause AI

> AI Powered Incident Investigation System using Coral

Root Cause AI is an intelligent incident investigation platform that helps developers identify production issues faster by correlating data across multiple tools like GitHub, Slack, Sentry, Datadog, Jira, and more using Coral.

Instead of manually checking logs, pull requests, monitoring dashboards, and team discussions separately, Root Cause AI brings everything together into one unified investigation workflow.

Built for the WeMakeDevs x Coral Hackathon.

---

# The Problem

Modern engineering teams work across fragmented systems.

When a production issue happens, developers usually need to:

* Check Sentry for errors
* Look at recent GitHub PRs
* Open Datadog dashboards
* Search Slack discussions
* Verify deployment timelines
* Read Jira tickets
* Ask teammates for context

This process is:

* slow
* repetitive
* mentally exhausting
* expensive for companies

The biggest challenge is not fixing the bug.

The biggest challenge is finding the right context quickly.

---

# Why Existing Workflows Fail

Every tool stores only a small part of the story.

| Tool    | Information        |
| ------- | ------------------ |
| GitHub  | Code changes       |
| Sentry  | Runtime errors     |
| Slack   | Team discussions   |
| Datadog | Metrics and spikes |
| Jira    | Tasks and tickets  |
| Notion  | Documentation      |

Developers manually connect these pieces in their heads.

This leads to:

* longer downtime
* slower debugging
* delayed incident response
* increased operational stress

---

# Our Solution

Root Cause AI uses Coral to unify all these systems through SQL.

Instead of writing custom integrations or switching between tabs, the system performs cross source queries and allows AI to reason over the complete operational context.

Example:

```sql
SELECT 
    pr.title,
    s.error_message,
    sl.message
FROM github.pull_requests pr
JOIN sentry.issues s
ON s.first_seen >= pr.merged_at
JOIN slack.messages sl
ON sl.channel = '#incidents'
WHERE s.level = 'fatal'
ORDER BY s.first_seen DESC;
```

The AI then:

* analyzes the joined data
* identifies probable root causes
* generates investigation summaries
* suggests likely impacted services

---

# Key Features

## Multi Source Incident Investigation

Connect and correlate data from:

* GitHub
* Slack
* Sentry
* Datadog
* Jira
* Notion
* PostgreSQL
* Any Coral compatible source

---

## AI Powered Root Cause Detection

The AI can:

* identify suspicious deployments
* detect error spikes
* summarize incident discussions
* map failures to code changes
* explain incidents in natural language

---

## Cross Source SQL Queries

Instead of multiple API calls:

```bash
GitHub API
Slack API
Sentry API
Datadog API
```

Everything becomes queryable as SQL tables.

---

## Timeline Reconstruction

The platform automatically builds incident timelines:

* Deployment happened
* Error rates increased
* Slack alerts triggered
* Team discussed rollback
* Service recovered

---

## Operational Context Engine

Root Cause AI gives developers:

* recent deployments
* related discussions
* impacted services
* logs and metrics
* suspected root cause

inside a single interface.

---

# Why Coral?

Coral solves the hardest problem in AI systems:
unifying fragmented operational data.

With Coral:

* every API becomes SQL
* cross source joins become possible
* auth and pagination are abstracted away
* AI agents receive structured context
* data stays local

This allows Root Cause AI to focus on reasoning instead of integration complexity.

---

# System Architecture

```text
                   +-------------------+
                   |    Frontend UI    |
                   +---------+---------+
                             |
                             v
                   +-------------------+
                   |  Spring Boot API  |
                   +---------+---------+
                             |
                             v
                   +-------------------+
                   |   AI Reasoning    |
                   | OpenAI / Claude   |
                   +---------+---------+
                             |
                             v
                   +-------------------+
                   |       Coral       |
                   +---------+---------+
                             |
        ------------------------------------------------
        |         |          |          |              |
        v         v          v          v              v
     GitHub     Slack     Sentry    Datadog         Jira
```

---

# Tech Stack

## Backend

* Java
* Spring Boot
* Spring AI
* REST APIs

## AI Layer

* OpenAI API / Claude API

## Query Layer

* Coral

## Frontend

* React / Next.js

## Database

* PostgreSQL

## Deployment

* Docker
* Render / Railway / AWS

---

# Example Workflow

## Scenario

A payment service starts failing after deployment.

The developer asks:

> "Why are payments failing?"

---

## Root Cause AI performs:

### Step 1

Checks recent GitHub merges.

### Step 2

Finds fatal Sentry issues after deployment.

### Step 3

Checks Slack incident discussions.

### Step 4

Correlates metrics from Datadog.

### Step 5

Generates AI summary.

---

## AI Generated Response

```text
Possible Root Cause Identified

A deployment merged 42 minutes before the first payment failure introduced changes in PaymentService.java.

Sentry shows a NullPointerException in transaction validation logic.

Slack discussions in #incidents mention rollback attempts and database timeout spikes.

Datadog metrics show increased latency immediately after deployment.

Most probable cause:
Recent payment validation update introduced a null handling regression.
```

---

# Future Improvements

* Automatic rollback suggestions
* Kubernetes integration
* Live anomaly detection
* CI/CD integration
* Voice incident assistant
* Predictive incident analysis
* AI generated remediation steps

---

# Impact

Root Cause AI can help teams:

* reduce debugging time
* reduce downtime
* improve developer productivity
* improve incident response
* reduce operational fatigue

Even reducing incident investigation time by a few minutes can save companies significant engineering effort and revenue.

---

# Challenges Faced

* Handling cross source context correlation
* Structuring AI prompts effectively
* Building reliable incident timelines
* Managing multi source query complexity
* Reducing hallucinations in AI reasoning

---

# What We Learned

* AI systems are only as good as their context
* Cross source querying is extremely powerful
* Coral simplifies data integration dramatically
* Operational intelligence is a major real world AI opportunity

---

# Getting Started

## Clone Repository

```bash
git clone https://github.com/yourusername/root-cause-ai.git
```

---

## Install Dependencies

```bash
cd root-cause-ai
npm install
```

or for backend:

```bash
mvn install
```

---

## Configure Coral Sources

```bash
coral source add github
coral source add slack
coral source add sentry
```

---

## Start Application

```bash
npm run dev
```

or

```bash
mvn spring-boot:run
```

---

# Team

Built with curiosity, caffeine, and production anxiety.

---

# Hackathon Submission

WeMakeDevs x Coral Hackathon 2026 - Shivansh Bagga

Track:
Enterprise Agent

Theme:
AI Powered Cross Source Incident Investigation

---

# License

MIT License
