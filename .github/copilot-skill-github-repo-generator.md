# GitHub Repository Generator

> Professional README generation and GitHub repository setup skill

## Trigger Conditions

**Use when:**
- "push to github", "create repo", "generate readme"
- "add topics", "setup repository", "document project"

**Skip when:**
- Simple git operations (commit, pull, push to existing)
- Repository already fully configured

## Execution Steps

### Step 1: Analyze Project

```bash
# Identify project type
ls -la
cat package.json 2>/dev/null || cat requirements.txt 2>/dev/null || cat Cargo.toml 2>/dev/null || cat go.mod 2>/dev/null || echo "Generic project"
```

Detect:
| File | Project Type |
|------|-------------|
| package.json | Node.js/JavaScript |
| requirements.txt, setup.py | Python |
| Cargo.toml | Rust |
| go.mod | Go |
| pom.xml, build.gradle | Java |
| *.csproj | C#/.NET |
| *.pkt | Cisco Packet Tracer |
| *.tex | LaTeX/Academic |
| docker-compose.yml | Docker |

### Step 2: Generate README

**Structure (No Emojis):**

```markdown
# [Project Title]

## Project Information
[Table with Author, Technology, Date, etc.]

---

## Overview
[2-3 paragraphs describing purpose and features]

---

## Table of Contents
[Auto-generated links]

---

## [Technical Sections]
- Architecture/Topology (for infra projects)
- Features (for software)
- Installation
- Usage
- Configuration
- API Reference (if applicable)
- Testing

---

## Repository Contents
[File/folder descriptions]

---

## License/Author Info
```

### Step 3: Generate Description

**Format (max 350 chars):**
```
[What it does] using [technologies] - [key features] | [domain/category]
```

**Examples:**
- `Enterprise network design using Cisco Packet Tracer - Multi-area OSPF, VLANs, VLSM | Computer Networks`
- `REST API with Node.js and Express - Authentication, CRUD operations, rate limiting | Backend Development`
- `ML pipeline for image classification using PyTorch - Data augmentation, transfer learning | Deep Learning`

### Step 4: Select Topics

Choose 10-20 from relevant categories:

**Languages:** python, javascript, typescript, java, go, rust, cpp, csharp
**Frameworks:** react, vue, angular, django, flask, express, spring-boot, nextjs
**Databases:** postgresql, mysql, mongodb, redis, sqlite, firebase
**DevOps:** docker, kubernetes, aws, azure, terraform, github-actions
**Networking:** cisco, ospf, vlan, routing, switching, network-design, firewall
**AI/ML:** machine-learning, deep-learning, tensorflow, pytorch, nlp, data-science
**Web:** web-development, frontend, backend, fullstack, api, rest-api
**Mobile:** android, ios, react-native, flutter
**Domain:** healthcare, fintech, e-commerce, education, iot, blockchain
**Type:** open-source, portfolio, tutorial, cli, library, boilerplate

### Step 5: Create Repository

```bash
# Initialize if needed
git init
git add .
git commit -m "feat: [description]

Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>"

# Create and push
gh repo create [name] --public --description "[description]" --source=. --remote=origin --push

# Add topics
gh repo edit [owner]/[name] --add-topic topic1 --add-topic topic2 ...
```

### Step 6: Verify

```bash
gh repo view [owner]/[name]
```

## Output Format

```
Repository: https://github.com/[user]/[repo]
Description: [Generated description]
Topics: [list of topics]
README: [sections included]
```

## Style Rules

| Do | Don't |
|----|-------|
| Use tables for data | Use emojis |
| Professional tone | Casual language |
| Code blocks with highlighting | Placeholder text |
| Proper heading hierarchy | Unnecessary sections |
| Horizontal rules between sections | Broken badges |
