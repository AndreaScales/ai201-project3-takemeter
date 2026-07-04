# ai201-project3-takemeter
Project 3 for CodePath AI201

## Evaluation Summary

The fine-tuned classifier performed best on **Recommendation**, which it labeled perfectly in the test set. The main errors happened at the boundary between **Analysis**, **Hot Take**, and **Reaction**, where the model sometimes over-weighted tone and under-weighted whether a post was actually supported by evidence.

![Confusion matrix](Confusion_matrix.png)

### What the matrix shows

- **Analysis** was usually correct, but 2 examples were pushed into **Hot Take**.
- **Hot Take** was the most ambiguous class: 1 example was read as **Analysis** and 1 as **Recommendation**.
- **Reaction** was also vulnerable to tone-based confusion, with 3 examples mislabeled as **Hot Take**.
- **Recommendation** was the cleanest class and did not produce any errors.

### Three representative mistakes

The confusion matrix does not expose the exact test rows, so these are three representative examples that match the failure modes shown above.

1. **Analysis misread as Hot Take**: "The article compares two albums and points to production choices for context."
	This sounds opinionated because it uses comparison language, but the real label is **Analysis** because it is still grounded in concrete evidence. The model likely focused on the evaluative tone and missed the fact that the sentence is explaining *why* the comparison matters.

2. **Reaction misread as Hot Take**: "That verse hit way harder than I expected."
	This is a fast emotional response, which belongs in **Reaction**, but it can look like a **Hot Take** because it is short, strong, and judgmental. The model appears to struggle when a reaction has the same surface style as a bold opinion.

3. **Hot Take misread as Recommendation**: "FRESH ALBUM Retch FINESSE THE WORLD 2"
	This kind of post sits close to **Recommendation** because it names a project and looks like a music prompt, even though it is really more of a blunt statement than a suggestion. The model seems to over-interpret release-style wording as a recommendation signal.

### Takeaway

Most of the remaining errors come from posts that are very short and rely on tone instead of explicit reasoning. The best way to improve this model further would be to add more examples that separate:

- evidence-based explanation vs. strong opinion,
- emotional reaction vs. blunt judgment,
- release announcements vs. true recommendations.
