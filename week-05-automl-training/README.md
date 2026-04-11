# Week 5: AutoML & No-Code Model Training

Trained a custom image classifier with Google Teachable Machine and compared
generic vs fine-tuned Hugging Face models for the Feed Collector component of our Threat Intelligence Feed Dashboard project.

## Custom Model Training
- Built a [Phishing/Legitimate] image classifier with Teachable Machine
- Achieved 100% accuracy on 10 held-out test images
- Precision: 100% | Recall: 100% | F1: 100%

## Fine-Tuned Model Comparison
Compared 3 models (1 generic + 2 fine-tuned) on 5 test inputs:
- Generic: distilbert-sst-2 (sentiment)
- Fine-Tuned A: ealvaradob/bert-finetuned-phishing (phishing detection)
- Fine-Tuned B: mrm8488/bert-tiny-finetuned-sms-spam-detection (spam detection)

## Finding
Recommended ealvaradob/bert-finetuned-phishing for Feed Collector because it is specifically trained for phishing detection and it outputs accurate classifications. Fine-tuned models showed higher performance with more relevant labels and better handling of edge cases.

See `report.md` for full analysis.
