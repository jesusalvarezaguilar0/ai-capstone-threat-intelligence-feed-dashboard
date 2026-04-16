# Model Comparison Report — Week 4

**Name:** Harry Yachimba  
**Date:** 3/26/2026  
**Capstone Project:** Threat Intelligence Feed Dashboard  
**My Component:** AI Summarizer & IOC Extractor  

## Test Setup

**Input dataset:** 5 cybersecurity text samples covering:
- 2 clearly concerning/high-severity records (unauthorized login, SSH attack)
- 1 ambiguous/edge case record (phishing email)
- 2 routine/benign records (firewall update, normal system utilization)

**Models tested:**
1. distilbert-base-uncased-finetuned-sst-2-english (sentiment)
2. facebook/bart-large-mnli (zero-shot classification)
3. dslim/bert-large-NER (named entity recognition)
4. Groq Llama 3 8B (LLM classification)

**Evaluation criteria:** label accuracy, usefulness for summarization/IOC extraction, confidence score, speed, ease of integration in n8n

## Results Summary

| Record | Sentiment | Zero-Shot | NER Entities | Groq |
|--------|----------|-----------|-------------|------|
| 1 | POSITIVE (0.7481) | routine activity | IP, location | INFORMATIONAL |
| 2 | POSITIVE (0.7481) | possible anomaly | organization | INFORMATIONAL |
| 3 | POSITIVE (0.7481) | critical threat | domain/org | LOW |
| 4 | POSITIVE (0.7481) | possible anomaly | location | CRITICAL |
| 5 | POSITIVE (0.7481) | routine activity | person | INFORMATIONAL |

## Analysis

**Where models agreed:**  
The zero-shot and Groq models generally agreed on routine records (records 1 and 5), classifying them as low-risk or informational.

**Where models disagreed:**  
The models disagreed on phishing and attack-related inputs. The zero-shot model labeled phishing as a critical threat, while Groq classified it as low severity. The sentiment model failed entirely by labeling all inputs as positive, showing it cannot distinguish security context.

**Most accurate model overall:**  
The Groq LLM was the most accurate because it provided meaningful severity classification along with reasoning, which is important for summarizing threat intelligence.

**Fastest/most practical:**  
The Hugging Face models were faster and easier to integrate, but Groq produced more useful outputs for real-world applications.

## Recommended Models for My Capstone Component

**Component:** AI Summarizer & IOC Extractor  

**Primary model:** Groq Llama 3 8B — generates contextual summaries and provides severity classification, making it ideal for summarizing threat intelligence feeds  

**Secondary model (if applicable):** dslim/bert-large-NER — extracts important entities such as IP addresses, locations, and organizations that can be used as IOCs  

**Rejected models and why:**
- distilbert-sst-2: Not useful because it does not understand cybersecurity context  
- bart-large-mnli: Useful for classification, but does not provide summaries or detailed reasoning  

## Failure Cases and Limitations

The sentiment model consistently misclassified all records as positive, including clearly malicious activity. Additionally, the zero-shot model sometimes overestimated or underestimated severity. The NER model, while useful for extracting entities, does not differentiate between relevant and irrelevant entities, which may require additional filtering in production.

## Next Steps

Future improvements include testing models specifically designed for cybersecurity threat detection, improving summarization quality, and combining NER outputs with LLM-generated summaries to enhance IOC extraction. Expanding the dataset and testing real-world threat intelligence feeds would also improve reliability.
