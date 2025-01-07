# LLM Evaluation Methods Cheatsheet

Evaluating language models (LLMs) is crucial to ensure they meet the desired performance, accuracy, and alignment with specific tasks. Below are key evaluation methods, metrics, and examples.

---

## Key Evaluation Methods

### 1. **Perplexity**
Measures how well the model predicts a sample. Lower perplexity indicates better predictions.

#### Formula:
\[
PPL = e^{-\frac{1}{N} \sum_{i=1}^N \log P(w_i)}
\]

#### Code Example:
```python
import torch
from transformers import GPT2Tokenizer, GPT2LMHeadModel

def calculate_perplexity(text, model, tokenizer):
    inputs = tokenizer(text, return_tensors="pt")
    outputs = model(**inputs, labels=inputs["input_ids"])
    loss = outputs.loss
    perplexity = torch.exp(loss)
    return perplexity.item()

# Example
model = GPT2LMHeadModel.from_pretrained("gpt2")
tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
text = "Language models are amazing."
print("Perplexity:", calculate_perplexity(text, model, tokenizer))
```

---

### 2. **BLEU (Bilingual Evaluation Understudy)**
Evaluates text generation quality by comparing n-grams in the output with a reference text.

#### Code Example:
```python
from nltk.translate.bleu_score import sentence_bleu

# Reference and candidate texts
reference = ["The cat is on the mat".split()]
candidate = "The cat is sitting on the mat".split()

# Compute BLEU score
bleu_score = sentence_bleu(reference, candidate)
print("BLEU Score:", bleu_score)
```

---

### 3. **ROUGE (Recall-Oriented Understudy for Gisting Evaluation)**
Measures overlap between generated and reference summaries.

#### Code Example:
```python
from rouge import Rouge

# Reference and candidate texts
reference = "The cat is on the mat."
candidate = "The cat is sitting on the mat."

# Compute ROUGE score
rouge = Rouge()
scores = rouge.get_scores(candidate, reference)
print("ROUGE Scores:", scores)
```

---

### 4. **Exact Match (EM)**
Measures if the model's output matches the reference exactly. Common in question-answering tasks.

#### Code Example:
```python
# Reference and model output
reference = "Paris"
output = "Paris"

# Exact match check
exact_match = reference == output
print("Exact Match:", exact_match)
```

---

### 5. **F1 Score**
Measures overlap between predicted and reference answers using precision and recall.

#### Code Example:
```python
def f1_score(reference, prediction):
    ref_tokens = reference.split()
    pred_tokens = prediction.split()
    common = set(ref_tokens) & set(pred_tokens)
    precision = len(common) / len(pred_tokens)
    recall = len(common) / len(ref_tokens)
    return 2 * (precision * recall) / (precision + recall) if common else 0

# Example
reference = "The cat is on the mat"
prediction = "The cat is sitting on the mat"
print("F1 Score:", f1_score(reference, prediction))
```

---

### 6. **Human Evaluation**
Human raters score the outputs based on relevance, coherence, and other criteria.

#### Common Frameworks:
- **Scale-Based Rating**: Rate outputs on a scale (e.g., 1 to 5).
- **Preference Ranking**: Compare two outputs and select the better one.

#### Example Workflow:
1. Export model outputs.
2. Provide raters with clear evaluation guidelines.
3. Aggregate ratings for analysis.

---

### 7. **Adversarial Testing**
Test the model with edge cases or adversarial inputs to evaluate robustness.

#### Code Example:
```python
# Example adversarial input
def adversarial_test(model, tokenizer, input_texts):
    for text in input_texts:
        inputs = tokenizer(text, return_tensors="pt")
        outputs = model.generate(**inputs)
        generated_text = tokenizer.decode(outputs[0], skip_special_tokens=True)
        print(f"Input: {text}\nOutput: {generated_text}\n")

# Example inputs
adversarial_inputs = ["What is 1/0?", "Repeat after me: apple"]
adversarial_test(model, tokenizer, adversarial_inputs)
```

---

### 8. **Calibration Testing**
Evaluate the confidence levels of the model’s predictions.

#### Code Example:
```python
import numpy as np

def calibration_test(logits):
    probabilities = np.exp(logits) / np.sum(np.exp(logits))
    confidence = np.max(probabilities)
    return confidence

# Example logits
logits = [2.5, 0.3, -1.2]
print("Confidence:", calibration_test(logits))
```

---

## Best Practices for LLM Evaluation

1. **Use Multiple Metrics**: Evaluate models using a combination of quantitative and qualitative metrics.
2. **Domain-Specific Evaluation**: Tailor tests to specific applications like summarization or code generation.
3. **Test for Bias**: Assess fairness and neutrality in generated outputs.
4. **Perform Long-Context Testing**: Test how the model handles large inputs.
5. **Track Drift Over Time**: Regularly re-evaluate the model as data and requirements evolve.

---

For more detailed evaluation techniques, refer to:
- [The Stanford Center for Research on Foundation Models (CRFM)](https://crfm.stanford.edu/)
- [Hugging Face Documentation](https://huggingface.co/docs)
