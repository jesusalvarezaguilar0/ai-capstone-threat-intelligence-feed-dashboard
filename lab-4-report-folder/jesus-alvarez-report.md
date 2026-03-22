# Model Comparison Report — Week 4

**Name:** Jesus Alvarez Aguilar
**Date:** 3/21/24
**Capstone Project:** Threat Intelligence Feed Dashboard 
**My Component:** Component 1 - Feed Collector

## Test Setup

**Input dataset:** 5 domain text samples covering cybersecurity alerts:
- 2 clearly concerning/high-severity records
    - Unauthorized login from IP 198.51.100.23 detected in admin account	
    - Multiple failed SSH attempts from Beijing IP on Cloudflare production server — 47  attempts in 5 minutes
- 1 ambiguous/edge case record
    - Phishing email with spoofed Amazon domain detected targeting                finance@acmecorp.com
- 2 routine/benign records
    - Routine firewall rule update completed on fw-01 during scheduled maintenance window
    - System resource utilization normal across all monitored hosts — no anomalies detected

**Models tested:**
1. distilbert-base-uncased-finetuned-sst-2-english (sentiment)
2. facebook/bart-large-mnli (zero-shot classification)
3. dslim/bert-large-NER (named entity recognition)
4. Groq Llama 3 8B (LLM classification)

**Evaluation criteria:** label accuracy, confidence score, speed, ease of
integration in n8n

## Results Summary

| Record | Sentiment | Zero-Shot | NER Entities | Groq |
|--------|-----------|-----------|-------------|------|
| 1 | Negative (0.9975) | Possible Anomaly | None | Critical |
| 2 | Negative (0.9986) | Routine Activity   | None | Informational |
| 3 | Negative (0.9959) | Possible Anomaly | Amazon (organization) | Medium |
| 4 | Negative (0.9994) | Possible Anomaly | SS (Misc)  | High |
| 5 | Negative (0.9880) | Routine Activity    | None | Informational |
 
## Analysis

**Where models agreed:** 
The models generally agreed on records 1, 3, and 4, which were all concerning security alerts. These records dealt with unauthorized login attempts, phishing activities, and repeated SSH login failures (brute force attack). The sentiment model labeled them as negative, the zero-shot model labeled them as possible anomalies, and the Groq LLM labeled them with a higher severity level. 

**Where models disagreed:** 
There were disagreements in records 2 and 5 because those records were describing routine system behaviors. The sentiment model labeled them as negative because the language used in the input text contained technical security verbiage. However, the zero-shot model and the Groq LLM were able to correctly label the events as routine or informational. 

**Most accurate model overall:** 
The Groq LLM gave the most useful classification for cybersecurity alerts. It was able to accurately label the records based on their severity levels, such as Critical, High, Medium, and Informational. 

**Fastest/most practical:** 
The Groq LLM would be the most practical model to use in the capstone project. It was able to give accurate severity classifications for all of the records compared to the Hugging Face model. The HF model needs more interpretation before its outputs can be put to use. 

## Recommended Models for My Capstone Component

**Component:** Feed Collector

**Primary model:** 
Groq Llama 3 8B - This model can classify incoming threat alerts by severity, and it allows for the quick prioritization of critical events. 

**Secondary model (if applicable):** 
facebook/bart-large-mnli (Zero-Shot Classification) - The zero-shot model can be a secondary classifier because it can categorize alerts into a broader range of groups. It can label them as routine activities or possible anomalies. 

**Rejected models and why:**
distilbert sentiment model - This sentiment model was not able to reliably and accurately able to tell the difference between a routine activity and an actual threat when the record had technical verbiage inside the input text. 

dslim/bert-large-NER model - This NER model was not able to identify all NER entities in all of the records. It wasn't able to pick up important names and places clearly stated in the records input text for a high-severity threat. 

## Failure Cases and Limitations

One model that gave me a wrong and surprising result was in record 4 during the NER entity model. The record was describing a brute force attack that clearly stated the name of an organization and a location, but the NER entity model only gave the abbreviation of the type of attack it was. Which is useful, but it does not give the full context for the high-severity alert.

## Next Steps

If I had more time, I would test a larger dataset of security alerts, using specific cybersecurity entity recognition models, adding more detailed classification labels for the threats, and adding more LLM models specifically for threat intelligence analysis.

