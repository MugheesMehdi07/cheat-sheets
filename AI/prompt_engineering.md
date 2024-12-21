# Prompt Engineering Cheatsheet

## Table of Contents
1. **Introduction**
2. **Prompt Strategies**
   - Few-shot Learning
   - Zero-shot Learning
   - Instruction-based Prompts
   - Chain-of-Thought Prompts
   - Role-playing Prompts
   - Constraint-based Prompts
   - Multi-modal Prompts
   - Iterative Refinement
3. **Detailed Examples for Each Strategy**
4. **Best Practices for Effective Prompting**
5. **Common Challenges and Solutions**
6. **Advanced Techniques and Tools**
7. **Frameworks for Prompt Engineering**
   - AUTOMAT Framework
   - CO.START Framework

---

## 1. Introduction
Prompt engineering is the art and science of crafting inputs that guide language models to generate desired outputs. It involves experimenting with phrasing, context, and examples to maximize the effectiveness of the model. This cheatsheet provides a comprehensive overview of strategies, examples, and best practices to help you master prompt engineering.

---

## 2. Prompt Strategies

### 2.1 Few-shot Learning
Few-shot learning involves providing a few labeled examples within the prompt to guide the model in generating desired outputs. This is particularly useful for tasks requiring patterns or structure.

#### Characteristics:
- **When to use:** When the task requires examples for context.
- **Advantages:** Can improve performance for specialized or less common tasks.

#### Example:
```
Task: Translate English sentences to French.
1. I love programming. -> J'aime programmer.
2. How are you? -> Comment ça va ?
3. The weather is nice today. -> Le temps est agréable aujourd'hui.
Translate the following sentence:
4. Can you help me? ->
```

---

### 2.2 Zero-shot Learning
Zero-shot learning is asking the model to perform a task without providing any explicit examples. The effectiveness depends on the clarity of the task description.

#### Characteristics:
- **When to use:** For general or well-understood tasks.
- **Advantages:** Saves time; tests the model's intrinsic understanding.

#### Example:
```
Summarize this paragraph:
"Artificial Intelligence is transforming industries with its ability to automate tasks, provide insights, and enhance decision-making."
```

---

### 2.3 Instruction-based Prompts
These prompts rely solely on explicit instructions to guide the model, often without examples.

#### Characteristics:
- **When to use:** Tasks with clear requirements.
- **Advantages:** Simplifies prompt creation and avoids overloading the model with data.

#### Example:
```
Explain the concept of entropy in physics using simple language suitable for a 10-year-old.
```

---

### 2.4 Chain-of-Thought Prompts
Chain-of-thought (CoT) prompting encourages the model to reason through a problem step-by-step, improving accuracy on tasks requiring logical or sequential thinking.

#### Characteristics:
- **When to use:** For multi-step reasoning tasks like math, logic, or planning.
- **Advantages:** Enhances transparency and correctness in reasoning.

#### Example:
```
If a train travels 60 miles per hour for 2 hours, how far does it go? Explain your reasoning step by step.
```
**Expected Output:**
"First, determine the speed of the train, which is 60 miles per hour. Multiply this by the time traveled (2 hours). 60 x 2 = 120 miles. Therefore, the train travels 120 miles."

---

### 2.5 Role-playing Prompts
Role-playing prompts ask the model to assume a specific role or perspective to tailor the response to a particular domain or context.

#### Characteristics:
- **When to use:** Domain-specific tasks or creative scenarios.
- **Advantages:** Guides the model to provide expertise or match tone/style.

#### Example:
```
You are a financial advisor. Explain the benefits of investing in index funds to a beginner.
```

---

### 2.6 Constraint-based Prompts
These prompts impose explicit constraints on the model's output, such as word count, style, or format.

#### Characteristics:
- **When to use:** Tasks requiring strict adherence to format or length.
- **Advantages:** Provides more predictable outputs.

#### Example:
```
Write a haiku about autumn.
```
**Expected Output:**
"Leaves fall gently down
Golden whispers in the breeze
Autumn's soft embrace."

---

### 2.7 Multi-modal Prompts
For models that support multi-modal inputs, this strategy combines text with other data types such as images, audio, or structured data.

#### Characteristics:
- **When to use:** Tasks requiring analysis or description of non-textual content.
- **Advantages:** Expands the applicability of language models.

#### Example:
```
Describe this image: [Insert image of a beach].
```
**Expected Output:**
"A serene beach with golden sand, gentle waves, and a clear blue sky."

---

### 2.8 Iterative Refinement
This strategy involves progressively refining prompts based on the model's responses to improve output quality.

#### Characteristics:
- **When to use:** Complex or ambiguous tasks requiring experimentation.
- **Advantages:** Allows tailored, high-quality responses.

#### Example:
1. **Initial Prompt:**
   "Explain quantum computing."
2. **Refined Prompt:**
   "Explain quantum computing in simple terms with an example about qubits."

---

## 3. Detailed Examples for Each Strategy
### Few-shot Learning:
- Categorize text sentiment with examples.
- Translate multiple sentences into different languages.

### Zero-shot Learning:
- Direct summarization tasks.
- Generating creative content (e.g., story ideas).

### Instruction-based Prompts:
- "Write a persuasive essay on climate change."

### Chain-of-Thought:
- Solve algebraic equations step-by-step.

---

## 4. Best Practices for Effective Prompting
1. **Be Clear and Specific:**
   - Avoid vague or ambiguous language.
2. **Use Examples Judiciously:**
   - Include examples only when necessary.
3. **Iterate:**
   - Test and refine prompts multiple times.
4. **Set Constraints:**
   - Specify desired output length, tone, or structure.
5. **Add Context:**
   - Provide necessary background information.

---

## 5. Common Challenges and Solutions

### Challenge 1: Ambiguity
- **Problem:** Model generates irrelevant responses.
- **Solution:** Add explicit instructions or examples.

### Challenge 2: Excessive Output Length
- **Problem:** Model produces overly verbose answers.
- **Solution:** Impose word or sentence limits.

### Challenge 3: Lack of Focus
- **Problem:** Responses deviate from the task.
- **Solution:** Reframe the prompt to emphasize focus.

---

## 6. Advanced Techniques and Tools
- **Temperature Adjustment:** Control creativity by setting the model's temperature parameter.
- **Token Limits:** Specify input/output length restrictions to manage verbosity.
- **Fine-tuning:** Use domain-specific data to improve task performance.
- **Prompt Libraries:** Maintain reusable prompts for common tasks.

---

## 7. Frameworks for Prompt Engineering

### 7.1 AUTOMAT Framework
The AUTOMAT Framework is a systematic approach to designing effective prompts by focusing on key elements that influence the model's performance.

- **A**ct as a: Clearly define the role or persona the model should assume.
  - Example: "You are a scientist writing a research summary."
- **U**ser Persona: Describe the target audience or end user.
  - Example: "Explain quantum mechanics to a high school student."
- **T**ask: Clearly define the task the model needs to accomplish.
  - Example: "Summarize the following text in 50 words."
- **O**utput Format: Specify the desired structure or style of the output.
  - Example: "Provide a numbered list of key points."
- **M**odifiers: Add constraints such as word count, tone, or style.
  - Example: "Write in a professional tone."
- **A**pproach: Decide on strategies like Few-shot or Chain-of-Thought.
  - Example: "Use step-by-step reasoning to explain."
- **T**esting: Iterate and refine the prompt based on responses.
  - Example: "If results are unclear, rephrase and test again."

### 7.2 CO.START Framework
The CO.START Framework emphasizes iterative refinement and contextual clarity to enhance the model's output.

- **C**ontext: Provide background or supporting details for the task.
  - Example: "Based on the following passage, answer the question."
- **O**bjective: State the goal of the task explicitly.
  - Example: "Write an email requesting a meeting."
- **S**pecificity: Use precise language and requirements.
  - Example: "Limit the response to 100 words."
- **T**one: Specify the desired tone or style.
  - Example: "Adopt a formal tone."
- **A**udience: Define the target audience for the response.
  - Example: "Explain this to a beginner in the field."
- **R**ole: Assign a role to the model to guide its perspective.
  - Example: "You are a historian analyzing World War II."
- **T**emplate: Use structured prompts or templates to ensure clarity.
  - Example: "In 3 bullet points, summarize the article."

By combining these frameworks, you can systematically design prompts that are clear, targeted, and effective for a wide range of applications.


