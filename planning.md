# Planning Document: Classifying Discourse in Black Hip-Hop Culture

## Community

For this project, I chose the Reddit community **r/hiphopheads**. This community is one of the largest online forums dedicated to hip-hop music and Black hip-hop culture, where users discuss new album releases, artist interviews, lyrical analysis, rap battles, music production, cultural topics, and industry news.

This community is a strong fit for a text classification task because the discussions are highly varied. Some users write thoughtful analyses supported by lyrics or historical context, while others post quick emotional reactions, bold opinions, or recommendations for new music. These different styles of communication create meaningful categories that a machine learning model can learn to distinguish.

---

# Labels

## 1. Analysis

**Definition**

A post that supports its opinion or claim using specific evidence such as lyrics, production details, historical context, interviews, statistics, or comparisons between artists.

### Example Posts

- "Kendrick's use of recurring religious symbolism throughout *Mr. Morale & the Big Steppers* expands on themes introduced in *DAMN.*, showing his growth as a storyteller."

- "Metro Boomin's production has shifted toward layered percussion since *Heroes & Villains*, making his newer beats sound much fuller than his earlier work."

---

## 2. Hot Take

**Definition**

A post that expresses a strong opinion without providing meaningful evidence or reasoning.

### Example Posts

- "Drake has never made a classic album."

- "J. Cole is the most overrated rapper of this generation."

---

## 3. Reaction

**Definition**

A post whose primary purpose is expressing an immediate emotional response to music, news, performances, or events rather than making an argument.

### Example Posts

- "That beat switch was absolutely insane."

- "RIP Young Dolph. This one really hurts."

---

## 4. Recommendation

**Definition**

A post that primarily asks for or gives music recommendations instead of debating or analyzing artists.

### Example Posts

- "Looking for artists similar to Smino."

- "If you enjoy Freddie Gibbs, you should definitely listen to Boldy James."

---

# Hard Edge Cases

Some posts naturally fall between **Analysis** and **Hot Take**.

### Example

> "Kendrick completely washed Drake. Just look at how 'Not Like Us' dominated streaming and won five Grammys."

This post contains evidence but is also written as a bold opinion.

### Decision Rule

If the evidence genuinely supports the claim through explanation or reasoning, I will label it **Analysis**.

If the evidence is only mentioned briefly to reinforce an opinion without real discussion, I will label it **Hot Take**.

This decision rule will help maintain consistency during annotation.

---

# Data Collection Plan

I will collect posts from the following Reddit community:

- r/hiphopheads

My goal is to annotate approximately **200 posts**, aiming for roughly:

| Label | Target Examples |
|--------|----------------:|
| Analysis | 50 |
| Hot Take | 50 |
| Reaction | 50 |
| Recommendation | 50 |

Because real Reddit data is naturally imbalanced, the final counts may differ.

If one label is significantly underrepresented after collecting 200 posts, I will search older discussion threads or use Reddit's search feature with keywords that are more likely to produce examples from that category. If necessary, I will collect additional posts until every class contains enough examples for training.

---

# Evaluation Metrics

Accuracy alone is not sufficient because some labels may occur much more frequently than others.

I will evaluate my classifier using:

- **Accuracy** to measure overall correctness.
- **Precision** to determine how often predicted labels are correct.
- **Recall** to measure how many posts from each class are successfully identified.
- **F1-score** because it balances precision and recall, making it especially useful if the dataset becomes imbalanced.
- **Confusion Matrix** to understand which labels the model most frequently confuses, particularly between Analysis and Hot Take.

These metrics provide a more complete evaluation than accuracy alone.

---

# Definition of Success

I would consider the classifier successful if it achieves:

- Accuracy of **80% or higher**
- Macro F1-score of **0.75 or higher**
- Precision and Recall above **70%** for every label

For deployment in a real community moderation or analytics tool, I would expect an F1-score near **0.80** while maintaining consistent performance across all four labels.

The classifier would be useful if it can reliably distinguish evidence-based discussion from unsupported opinions, emotional reactions, and recommendation posts with minimal human correction.

# AI Tool Plan

## Label Stress-Testing

Before beginning annotation, I will use ChatGPT to test my label definitions by generating 5–10 example Reddit posts that intentionally fall between two labels, especially between **Analysis** and **Hot Take**. If I find examples that are difficult to classify consistently, I will revise my label definitions or decision rules before annotating the full dataset. This process will help ensure the labels are mutually exclusive and consistently applied.

---

## Annotation Assistance

I plan to use **ChatGPT (GPT-5.5)** to pre-label a small batch of Reddit posts before reviewing them manually. Every AI-generated label will be verified by me, and I will make the final annotation decision. I will keep a separate record of which examples were initially pre-labeled by AI so I can clearly disclose AI assistance in my project documentation.

---

## Failure Analysis

After evaluating my classifier, I will provide ChatGPT with examples of incorrect predictions along with the model's predicted labels and the correct labels. I will ask the AI to identify common error patterns, such as confusing **Analysis** with **Hot Take** or **Reaction** with **Recommendation**. I will verify each suggested pattern by manually reviewing the original Reddit posts and comparing them with my annotation guidelines before including any conclusions in my evaluation.