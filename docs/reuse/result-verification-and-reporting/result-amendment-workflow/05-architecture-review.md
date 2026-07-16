An amendment never overwrites the original finalized result — it creates
a new, linked `DiagnosticReport` version with status `amended`/
`corrected`, preserving the original as an immutable prior version (feeds
immudb, Module 3, for tamper-evident history) with a mandatory reason-
for-amendment field and re-notification of any party who received the
original report (reuses `critical-result-escalation`'s Novu channel if
the original was a critical result).
