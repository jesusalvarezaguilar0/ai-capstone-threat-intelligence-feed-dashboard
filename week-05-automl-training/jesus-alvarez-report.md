# Week 5 Report: AutoML Training & Fine-Tuned Model Evaluation

**Name:** Jesus Alvarez Aguilar

**Date:** 04/09/26

**Capstone Project:** Threat Intelligence Feed Dashboard (Cybersecurity)

**My Component:** Component 1 - Feed Collector

## Part A: Teachable Machine Training

### Training Setup
- **Task:** Phishing vs Legitimate email screenshot classification
- **Training images per class:** ~ 25
- **Test images per class:** ~ 5
- **Total training time:** ~30 seconds

### Test Results

| # | Actual Class | Predicted Class | Confidence | Correct? |
|---|--------------|-----------------|------------|----------|
| 1 | Phishing | Phishing | 100% | Yes |
| 2 | Phishing | Phishing | 76% | Yes |
| 3 | Phishing | Phishing | 100% | Yes |
| 4 | Phishing | Phishing | 99% | Yes |
| 5 | Phishing | Phishing | 70% | Yes |
| 6 | Legitimate | Legitimate | 99% | Yes |
| 7 | Legitimate | Legitimate | 100% | Yes |
| 8 | Legitimate | Legitimate | 99% | Yes |
| 9 | Legitimate | Legitimate | 100% | Yes |
| 10 | Legitimate | Legitimate | 100% | Yes |

### Confusion Matrix

| | Model Predicted: Phishing  | Model Predicted: Legitimate |
|---|---|---|
| **Actual: Phishing** | TP = 5 | FN = 0 |
| **Actual: Legitimate** | FP = 0 | TN = 5 |

### Calculated Metrics
- **Accuracy:** 100%
- **Precision:** 100%
- **Recall:** 100%
- **F1 Score:** 100%

### Interpretation
The model works equally well in both precision and recall, both got 100%. This means that it was able to correctly identify all phishing and legitimate samples without any false positives or false negatives. However, since there was only 25 screenshot examples per class, the sample size was small. To improve my model, I would use a larger and more diverse set of data so it has a bigger sample size.  

---

## Part B: Generic vs Fine-Tuned Model Comparison

### Models Tested
1. **Generic:** distilbert-base-uncased-finetuned-sst-2-english (sentiment)
2. **Fine-Tuned A:** ealvaradob/bert-finetuned-phishing — phishing detection model
3. **Fine-Tuned B:** mrm8488/bert-tiny-finetuned-sms-spam-detection —spam detection model

### Results

| Input | Generic Label (Score) | Fine-Tuned A Label (Score) | Fine-Tuned B Label (Score) | Best Model |
|------|----------------------|----------------------------|----------------------------|-----------|
| Unauthorized login attempt detected | POSITIVE (0.74) | phishing (1.00) | LABEL_0 (0.83) | Fine-Tuned A |
| Routine firewall update completed | POSITIVE (0.74) | benign (1.00) | LABEL_1 (0.53) | Fine-Tuned A |
| Phishing email detected in inbox | POSITIVE (0.74) | phishing (1.00) | LABEL_0 (0.74) | Fine-Tuned A |
| Multiple failed SSH attempts | POSITIVE (0.74) | benign (0.95) | LABEL_1 (0.57) | Fine-Tuned A |
| System resource usage spike | POSITIVE (0.74) | benign (0.99) | LABEL_0 (0.83) | Fine-Tuned A |


### Analysis

**Generic model strengths:** 
- The generic sentiment model performed consistently throughout all of the records in terms of confidence. It maintained a moderate confidence level of 74% throughout all of the 5 records. 

**Generic model weaknesses:** 
- The generic sentiment model failed to properly classify cybersecurity related inputs because it was designed for sentiment analysis rather than threat detection. The model outputted POSITIVE instead of outputting whether it was a phishing or benign. 

**Fine-tuned model advantage:** 
- The fine-tuned models outperformed the generic model by being able to correctly tell the difference between a phishing and benign record.

**Biggest surprise:** 
- I did not expect the generic model to give the same confidence score for all 5 records, I was expecting at least a small bit of deviation but it remained the same for all of the records. 

### Recommended Model for My Capstone Component

**Component:** Feed Collector

**Primary model:** ealvaradob/bert-finetuned-phishing 
- This model would be best for my task because it is specifically trained to detect phishing content. It can accurately classify incoming threat data as phishing or benign, which can help organize and filter data. 

**Confidence threshold:** 
- I would use a threshold of 90% to make sure that only reliable and safe classifications can be accepted, as this will improve the quality of the data. 

**Priority metric:** 
- Recall would matter most for my project because ensuring that it doesn't miss any false negatives could help prevent any damages caused by phishing content even if it occasionally flags benign content. 
---

## Limitations & Next Steps

With more time and data, I would use a larger dataset in order to include real-world cybersecurity inputs. My current dataset was small, with only 25 images per class and I would include more classes and images per class. I would also fine-tune my model using more domain-specific cybersecurity data to try to improve the accuracy and consistency of my model. I would test out more specialized models that are trained on threat detection to check how they compare.
