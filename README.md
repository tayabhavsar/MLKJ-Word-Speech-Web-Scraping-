# MLK Speech Word Frequency

A Python project that scrapes the text of a speech from a webpage, cleans it
up with regular expressions, and counts how often each word appears using
pandas. Built as hands-on practice combining three core skills: web scraping
(`requests` + `BeautifulSoup`), regex-based text cleaning, and data
aggregation with pandas. The example target is Dr. Martin Luther King Jr.'s
1963 "I Have a Dream" speech, but the approach works on any similar page of
text.

## What it does

1. **Scrape** — pulls the raw HTML from a webpage using `requests`, then
   uses `BeautifulSoup` to grab the text out of every `<p>` tag.
2. **Clean** — collapses line breaks, strips out punctuation with a regex
   (`[^\w\s]`), and lowercases everything so `"Freedom"` and `"freedom."`
   count as the same word.
3. **Count** — splits the cleaned text into words and tallies them with
   `pandas.Series.value_counts()`.
4. **Export** — saves the results to a CSV (word, count).

## Repo contents

- `WebScraping_Regex_Project.md` — the full step-by-step process: every cell,
  the intermediate outputs, and the reasoning behind each cleaning step
- `MLK_Speech_Counts.csv` — the final word-count results from running the
  process on the MLK speech
- `requirements.txt` — the packages needed to reproduce this (`requests`,
  `beautifulsoup4`, `pandas`)

## Results

The cleaned speech breaks down into 323 unique words. The most common:

| word | count |
|------|-------|
| the  | 54    |
| of   | 49    |
| to   | 29    |
| and  | 27    |
| a    | 20    |

Full results in [`MLK_Speech_Counts.csv`](./MLK_Speech_Counts.csv).

## How to reproduce

1. Install dependencies: `pip install -r requirements.txt`
2. Open `WebScraping_Regex_Project.md` and run through the steps in order —
   it walks through scraping the page, cleaning the text with regex, and
   counting words with pandas.

## Why this project

Built to practice three things together: web scraping (`requests` +
`BeautifulSoup`), regular expressions for text cleaning, and `pandas` for
aggregation — end to end, from a live webpage to a clean, countable dataset.

## Possible next steps

- Refactor the process into a reusable script with functions
- Add a CLI so it works on any URL, not just the MLK speech page
- Filter out common stopwords ("the", "of", "to"...) for a more meaningful
  frequency list
- Visualize the top words with a bar chart or word cloud

## License

MIT — see [LICENSE](./LICENSE).
