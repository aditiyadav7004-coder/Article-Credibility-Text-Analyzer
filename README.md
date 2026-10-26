# Article Credibility & Text Analyzer

A lightweight, client-side heuristic tool that scans an article's headline and body text and gives it a **credibility score out of 100**. It looks for sensational language, excessive punctuation and capitalization, source attribution, quotes, and numeric evidence.

Everything runs in the browser from a single HTML file. There is no backend, no build step, no dependencies, and no text ever leaves your machine.

> **Note:** This is a rule-based heuristic tool for learning and quick screening. It does **not** verify facts and cannot tell whether an article is true. See [Limitations](#limitations).

---

## Features

- **Credibility score (0-100)** with a colour-coded label
- **Text statistics:** word count, sentence count, caps ratio, exclamation/question marks, quotes and attributions, numeric data points
- **Linguistic indicator flags** explaining why the score went up or down
- **Sample article loader** to try the tool instantly
- **CSV export** of the analysis summary
- **Responsive layout** that works on desktop and mobile
- **100% offline:** just open the file in a browser

---

## Getting Started

### Run locally

```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>
```

Then open `index.html` in any modern browser. No installation needed.

### Usage

1. Enter the article headline (optional) and paste the body text.
2. Click **Analyze Text**.
3. Review the score, statistics, and linguistic indicators.
4. Click **Export CSV** to download a summary.
5. Use **Load Sample** to see an example, or **Clear** to reset.

---

## How Scoring Works

The score starts at **100** and points are deducted based on the rules below.

| Check | Condition | Penalty |
|---|---|---|
| Sensational language | Keywords like "shocking", "miracle", "conspiracy", "exposed" | 8 per match (max 30) |
| Excessive punctuation | More than 3 `!` or `?` in total | 5 per extra mark (max 20) |
| High capitalization | ALL-CAPS words exceed 3% of all words | 15 |
| No attribution | No quotes and no attribution phrases ("according to", "said", "reported", ...) | 20 |
| Low quantitative data | Text over 150 words with 2 or fewer numbers | 10 |

The final score is clamped between 0 and 100.

| Score | Label |
|---|---|
| 75 - 100 | High Credibility Indicators |
| 45 - 74 | Moderate Caution Advised |
| 0 - 44 | Low Credibility Indicators |

---

## Project Structure

```
.
├── index.html     # Entire app: HTML, CSS, and JavaScript
└── README.md
```

---

## Customization

Both keyword lists are plain arrays at the top of the `<script>` block, so you can edit them easily:

```js
const SENSATIONAL_WORDS = ["shocking", "unbelievable", "secret", ...];
const ATTRIBUTION_WORDS = ["according to", "said", "stated", ...];
```

Penalty values and score thresholds can be adjusted inside the `analyzeText()` function.

---

## Limitations

- It is a **heuristic**, not a fact-checker. A false article written in a calm, well-attributed style can score high, and a legitimate opinion piece can score low.
- Keyword matching is English-only and does not understand context or sarcasm.
- Sentence counting is a simple split on `.`, `!`, `?`, so abbreviations may inflate the count.
- The CSV export currently includes only the score, word count, sentence count, and caps ratio.

---

## Roadmap Ideas

- Source/domain reputation checks
- Readability scores (Flesch-Kincaid)
- Sentiment and subjectivity analysis
- Multi-language keyword support
- Highlighting flagged words directly in the text
- Full-metric CSV/JSON export

---

## Contributing

Contributions are welcome.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## License

This project is licensed under the [MIT License](LICENSE).
