---
type: llm
focus: mock_calls
arm: both
---

Look only at the crea_contenuto calls. PASS if there is one instagram_post and one separate instagram_storia, both linked to the wine-tasting event (evento_id) and scheduled between 11:00 and 13:30 on the same day, a day before the event date (2026-10-31); the post text states the date (31 October), the time (19:30), the price (45 €) and how to book; the story text is short (one or two sentences); and neither is set to APPROVATO.
FAIL if post and story are merged in one item, if the date, time, price or booking instruction is missing from the post, if the scheduled time is not lunchtime on a day before the event, or if a content item is APPROVATO.
