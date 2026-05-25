# Prompt Log — Jesus Alvarez Aguilar

**Project:** Threat Intelligence Automation Pipeline

**Team:** UGR 277 Capstone Team

**My Component:** Component 1 — Threat Feed Collector

**AI Tools Used:** GitHub Copilot, ChatGPT

---

# How to Use This Log

This log documents significant AI-assisted development activities used throughout the capstone project. Each entry records the context, prompt, result, evaluation, modifications made, and lessons learned while using AI tools to improve workflows, documentation, testing, and integration.

---

## 2026-04-22 — Building Alert Classifier Prompt

### Context
Creating the first Flowise chain responsible for classifying cybersecurity alerts into severity levels.

### Prompt
> Create a system prompt for a cybersecurity alert classifier that outputs JSON containing severity, confidence, and reasoning.

### Result
Generated a structured prompt with severity categories and JSON formatting instructions.

### Evaluation
The output worked well and produced consistent JSON responses. Some severity definitions were too broad.

### What I Changed
Added custom severity definitions and restricted outputs to CRITICAL, HIGH, MEDIUM, LOW, and INFO.

### What I Learned
Explicit constraints improve consistency and make outputs easier to process downstream.

---

## 2026-04-22 — Improving Threat Analyzer Output Structure

### Context
Developing the second Flowise chain that performs threat analysis.

### Prompt
> Generate a JSON schema for cybersecurity threat analysis including attack type, indicators, impact, and MITRE ATT&CK techniques.

### Result
Produced a detailed JSON structure for threat intelligence analysis.

### Evaluation
The structure was useful but occasionally generated MITRE techniques that were not supported by evidence.

### What I Changed
Added instructions to return "unknown" when no MITRE technique could be confidently identified.

### What I Learned
Preventing the model from guessing improves reliability.

---

## 2026-04-22 — Creating Response Recommendation Chain

### Context
Building the final Flowise chain responsible for incident response recommendations.

### Prompt
> Create a prompt that generates actionable incident response steps based on a cybersecurity threat analysis.

### Result
Generated immediate actions, investigation steps, containment strategy, and escalation guidance.

### Evaluation
Recommendations were useful but sometimes too generic.

### What I Changed
Added instructions requiring specific actions instead of vague recommendations.

### What I Learned
Specificity requirements significantly improve practical usefulness.

---

## 2026-04-23 — Connecting Flowise Chains to n8n

### Context
Integrating Flowise APIs into an n8n workflow.

### Prompt
> Show how to send data from one Flowise chain into another using n8n HTTP Request nodes.

### Result
Received example HTTP configurations and JSON request formats.

### Evaluation
The example worked after minor modifications to field mappings.

### What I Changed
Updated JSON expressions to reference the previous node's text output correctly.

### What I Learned
Understanding output structure is critical when chaining multiple AI services together.

---

## 2026-04-23 — Debugging Flowise API Responses

### Context
The HTTP Request node was returning unexpected results.

### Prompt
> Why does my Flowise API return text instead of structured fields?

### Result
Explained that Flowise returns the model response inside a text property.

### Evaluation
Correct diagnosis.

### What I Changed
Adjusted n8n expressions to read from the text field.

### What I Learned
Always inspect actual API responses before designing expressions.

---

## 2026-04-24 — Generating Copilot Project Instructions

### Context
Creating .github/copilot-instructions.md for the capstone repository.

### Prompt
> Create a GitHub Copilot instructions file for a cybersecurity threat intelligence automation platform using n8n, Airtable, Groq, and Flowise.

### Result
Generated a detailed project context document.

### Evaluation
Good structure but lacked project-specific details.

### What I Changed
Added actual Airtable fields, component responsibilities, and workflow descriptions.

### What I Learned
Providing project context dramatically improves AI-generated recommendations.

---

## 2026-04-24 — Performing Capstone Audit

### Context
Evaluating readiness for Checkpoint 2.

### Prompt
> Act as a capstone advisor and identify gaps that would prevent end-to-end automation across four components.

### Result
Generated a readiness assessment with risk areas and recommendations.

### Evaluation
The audit correctly identified integration testing as the highest priority.

### What I Changed
Assigned ownership of fixes to individual team members.

### What I Learned
External reviews help reveal issues that teams often overlook.

---

## 2026-04-25 — Creating Component README

### Context
Documenting Component 1 for the capstone repository.

### Prompt
> Write a professional README describing a cybersecurity threat feed collection system built with n8n and Airtable.

### Result
Generated a structured README including overview, setup instructions, and testing procedures.

### Evaluation
Strong starting point but contained generic examples.

### What I Changed
Replaced placeholders with actual workflow descriptions and screenshots.

### What I Learned
AI accelerates documentation creation but still requires verification and customization.

---

## 2026-04-25 — Generating Test Data

### Context
Need additional threat intelligence records for workflow testing.

### Prompt
> Generate realistic cybersecurity threat intelligence records including severity levels, URLs, timestamps, and summaries.

### Result
Produced a variety of realistic test records.

### Evaluation
Most examples were useful for testing workflow logic.

### What I Changed
Adjusted severity distributions and removed duplicate examples.

### What I Learned
AI-generated test data is valuable for quickly expanding test coverage.

---

## 2026-04-26 — Designing GitHub Portfolio Projects

### Context
Preparing repositories for portfolio presentation.

### Prompt
> Convert my Week 7 RAG chatbot and Week 8 LLM chain pipeline labs into professional GitHub portfolio projects.

### Result
Generated project descriptions, README structures, and portfolio recommendations.

### Evaluation
The recommendations aligned well with portfolio best practices.

### What I Changed
Customized descriptions to reflect actual implementation details and project outcomes.

### What I Learned
Presenting projects professionally is almost as important as building them.
