# MLK Speech Word Frequency

A Python project that scrapes the text of a speech from a webpage, cleans it
up with regular expressions, and counts how often each word appears using
pandas. Built as hands-on practice combining three core skills: web scraping
(`requests` + `BeautifulSoup`), regex-based text cleaning, and data
aggregation with pandas — refactored from an exploratory notebook into
reusable, testable functions. The example target is Dr. Martin Luther King
Jr.'s 1963 "I Have a Dream" speech, but the URL and HTML tag can be swapped
out to analyze any similar page of text.

## What it does

1. **Scrape** — pulls the raw HTML from a webpage using `requests`, then
   uses `BeautifulSoup` to grab the text out of every `<p>` tag.
2. **Clean** — collapses line breaks, strips out punctuation with a regex
   (`[^\w\s]`), and lowercases everything so `"Freedom"` and `"freedom."`
   count as the same word.
3. **Count** — splits the cleaned text into words and tallies them with
   `pandas.Series.value_counts()`.
4. **Export** — saves the results to a CSV (word, count).

## Project structure

```
mlk-speech-word-frequency/
├── README.md
├── requirements.txt
├── .gitignore
├── src/
│   └── word_frequency.py   # scrape -> clean -> count -> save pipeline
├── data/                   # (optional) place for saved/raw HTML if you cache it
└── output/                 # generated CSVs land here (ignored by git)
```

## Setup

```bash
git clone https://github.com/<your-username>/mlk-speech-word-frequency.git
cd mlk-speech-word-frequency
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Usage

Run with the defaults (scrapes the MLK speech page and saves to
`output/word_counts.csv`):

```bash
python src/word_frequency.py
```

Or point it at a different page / tag / output location:

```bash
python src/word_frequency.py --url "'http://analytictech.com/mb021/mlk.htm'" --tag p --out output/counts.csv
```

Sample output:

```
Saved 323 unique words to output/word_counts.csv

Top 10 most common words:
word
the    54
of     49
to     29
and    27
a      20
...
```

## Why this project

This started as a notebook exploration to practice three things together:
web scraping (`requests` + `BeautifulSoup`), regular expressions for text
cleaning, and `pandas` for aggregation. It's been refactored here into
reusable functions (`fetch_html`, `extract_text`, `clean_text`,
`count_words`) instead of one long notebook, so it's easier to read, test,
and reuse on a different speech or article.

## Possible next steps

- Add a `--top` flag to only print/save the top N words
- Filter out common stopwords ("the", "of", "to"...) for a more meaningful
  frequency list
- Add unit tests for `clean_text` and `count_words`
- Visualize the top words with a bar chart (matplotlib) or a word cloud

## License

MIT — see [LICENSE](LICENSE).
