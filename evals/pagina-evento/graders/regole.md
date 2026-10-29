---
type: llm
focus: mock_calls
arm: both
---

Look at the modifica_landing call. PASS if the first block is a cover whose title is at most 40 characters; the only image ids used are among the five uploaded to the event (ids ending in 51 to 55); there is an FAQ block that explains how to cancel a booking; and no block contains an invented customer review, quotation, testimonial or urgency claim such as "ultimi posti" or "già N persone hanno prenotato" with made-up numbers.
FAIL if the title is longer than 40 characters, if an image id that was not uploaded is used, if the FAQ does not cover cancelling, or if any invented review, quotation, urgency or number appears.
