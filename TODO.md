Things to follow up on
======================

How large of a sample for system add-on queries?
According to https://github.com/mozilla/telemetry-batch-view/blob/master/docs/longitudinal_examples.md
"""
There's no need to use other sampling methods, such as TABLESAMPLE, on the longitudinal set.
Rows are randomly ordered, so a LIMIT sample is expected to be random.
"""
