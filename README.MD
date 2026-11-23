# Book Sales & Ratings - Exploratory Analysis

## Question
What is associated with a book's sales and ratings: price, genre, author tier, publisher, publication year?

## Data
'Books_Data_Clean.csv': 1,070 books, 15 columns (sales, ratings, publisher, genre).
Publishing year is the year the edition/work came out, not when it sold.

## Cleaning (1,070 -> 988)
- Scope: kept works first published after 1900 (-61 rows which included books up to -560 Publishing Year; these are old classics, not errors)
- Dropped rows with no title (-21 rows); 0 exact duplicates
- Merged publisher spelling variants (9->8); mapped language codes to languages

## Findings 
1. Penguin earns ~$2,060 per book vs Amazon Digital Services ~$253. 
   61 % of Amazon's 561 books record $0 publisher revenue; no other publisher has any zeros.
   This looks like a recording difference, not low sales.
2. Author tier doesn't track ratings per book: Intermediate has the highest median (98k), Excellent among the lowest (82k)
3. Rating vs number of ratings: Spearman p=0.11, weak relationship/correlation.
4. Year: Total units peak for books published 2005–2012 because the dataset contains more books from those years; median units per book stays roughly flat.
5. Among authors with >= 3 books, the top 10 average 4.30-4.53. These gaps are about the size of the noise for 3-10 books, so the order within the top 10 isn't meaningful.

## Limitations
- Language is 99% English among known values; 47 unknown -> were not analysed as a variable
- Author strings include co-authors/translators ; rankings use first-listed author
- Small groups (Famous n=48, Novice n=28) give unstable estimates
- Revenue zeros at Amazon make revenue comparison across publishers partial

## Next steps toward modeling
- Target: log(units sold), because it is right-skewed
- Features known before sale: price, genre, author tier, publisher, year
- Excluded: gross sales, publisher revenue, sales rank (derived from sales -> leakage); language (near-constant)
- Baseline: predict the median, then linear regression, then gradient boosting; compare on a held-out set

## How to run
pip install -r requirements.txt, then open notebook.ipynb -> Restart and Run All