# Week 4: Model Comparison

Tested 4 AI models on 5 cybersecurity alert text samples to evaluate their suitability
for the Feed Collector component of our Threat Intelligence Feed Dashboard.

## Models Tested

- HF Sentiment (distilbert-sst-2)
- HF Zero-Shot (bart-large-mnli)
- HF NER (bert-large-NER)
- Groq Llama 3 8B

## Finding

Recommended Groq Llama 3 8B for the Feed Collector because it produced the most accurate security severity classification for the alerts. 

See `report.md` for full analysis.

