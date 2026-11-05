# Weekly keyword ranking log spreadsheet

A weekly keyword ranking log spreadsheet is a place to put one desktop Google check beside the previous one. The files in this repo are a template. The sample rows use `example.com` so the formulas have something to read. They are not a case study and not a client's results. Replace them.

The log is deliberately dull. Same keywords, same city, same device class, roughly the same weekday. A weekly keyword ranking log spreadsheet stops being comparable the moment a row silently changes city or starts mixing a phone screenshot with a desktop export.

What you record for each keyword on each run:

- the date of the check
- the keyword
- the region (country or city) saved on the project
- device class, written as `desktop` for these exports
- organic position, empty if the site was not found
- the ranking URL
- the position from the previous kept check
- the change, as a formula

Empty position means not found. Do not type `0`.

### Files

- `ranking-history-template.csv` — header plus two SAMPLE rows and a blank row.
- This README — Sheets formulas and the rules for the change column.

### Google Sheets

Import the CSV into a new Sheet. Put the header in row 1. Columns:

| Column | Field |
|---|---|
| A | date |
| B | keyword |
| C | region |
| D | device |
| E | position |
| F | ranking_url |
| G | previous_position |
| H | change |

`previous_position` can be typed from last week's column E, or filled with `=IF(B2="","",IFERROR(INDEX(FILTER(E:E,B:B=B2,A:A<A2),COUNTA(FILTER(E:E,B:B=B2,A:A<A2))),""))` if you stack every week in one tab and want the latest prior numeric cell. The simple version, for a sheet that is one week per tab, is to paste last week's positions into column G by hand.

Change, where a smaller position number is an improvement:

```
=IF(OR(E2="",G2=""),"",G2-E2)
```

Positive means the position number fell (closer to 1). Negative means it rose. An empty position leaves the change blank, so a not-found row does not look like a climb to position zero.

Other formulas, for the week currently in column E:

- Found rows: `=COUNT(E2:E500)`
- Average of found positions: `=IF(COUNT(E2:E500)=0,"",AVERAGE(E2:E500))`
- Top 3: `=COUNTIFS(E2:E500,">=1",E2:E500,"<=3")`
- Top 10: `=COUNTIFS(E2:E500,">=1",E2:E500,"<=10")`

Do not average a column that uses 100 as a stand-in for "not found" unless you label that choice in the sheet. It is not what an empty cell means.

### What the source check contains

The rows you paste should come from a desktop Google check for one region. The report also has visibility in percent, average position, Top 3 and Top 10 counts, the change since the previous check, and a saved results page with the site highlighted. An AI Overview citation is stored separately. It is not the organic position. Up to 10 competitors can sit on the project, and another tab lists sites that appear for the keywords. Charts in the cabinet appear after the second check. This sheet is the part you can mail and reopen without signing in.

Depth is Top 10, Top 30, Top 50, or Top 100. Pages after the first are loaded only until the site or a project competitor is found. Price is per keyword. From 4 tokens per keyword; until 2 December 2026 — 2 tokens. A first page that includes an AI Overview is 8 tokens at the full rate and 4 during the starting window. Tokens are charged only for a run that starts. They do not expire. There is no monthly minimum. An optional subscription adds 10% tokens. New accounts get 100 tokens. Packs start at $5.

One hundred keywords, four weekly checks, Top 10, no AI Overview premium: 1,600 tokens at the full rate, 800 at the starting rate. A weekly keyword ranking log spreadsheet does not add a fee on top of that. It stores the export.

The check itself is the [desktop Google rank report](https://en.speedyindex.com/google-rank-tracker/). Which lists deserve a weekly row, and which can wait a month, is discussed in [the frequency guide](https://uskotoivo81-netizen.github.io/how-often-small-site-checks-google-rankings/).

### FAQ

**Can I log two cities on one tab?**
Yes, if column C is filled and you never sort it away. A pivot or a filter that hides the city will make next month's comparison false. Separate tabs are harder to mix up.

**Does the change formula know about AI Overviews?**
No. Column E is the organic position only. Keep citations in a column you add yourself, and do not subtract them from E.

**What if last week was not found and this week is position 9?**
Leave G empty or type the word `none` and keep H blank. Do not subtract 9 from 100 unless your team has written down that convention.

**Is the sample data real?**
No. `example.com` rows are fixtures for the formulas. Delete them before you paste an export.
