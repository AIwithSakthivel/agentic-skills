# Docs And Logbook Pattern

Keep delivery documentation and internal notes separate.

`README.md` should contain:

- feature purpose
- dependencies
- inputs and outputs
- public API or run method
- examples of how to use the feature

Workbook should contain:

- design notes
- decisions and assumptions
- timestamped work log
- validation notes
- internal follow-ups

Logging rules:

- Always create `logs/` and `results/`.
- In Plan Mode, if the user has not defined logging expectations, ask what should be logged.
- Outside Plan Mode, use a sane default baseline and mention that assumption.

Suggested timestamp format:

- `YYYY-MM-DD HH:MM:SS TZ (+offset)`

Do not:

- mix internal change history into delivery README
- store long-lived prompts in README or workbook
- retire the workbook if the user wants future traceability
