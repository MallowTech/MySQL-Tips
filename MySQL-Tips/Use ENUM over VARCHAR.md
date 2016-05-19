---
Title: Use ENUM over VARCHAR
Tip-number: 3
Tip-username: Vijayanand
Tip-username-profile: https://github.com/vijayanandp
Tip-description: Use ENUM over VARCHAR
---

ENUM type columns are very fast and compact. Internally they are stored like TINYINT, but still they can contain and display string values.

If we have a field, which contains only a fixed number of values, use ENUM instead of VARCHAR. For example if we have a column named "Approval", and only contain values such as "Approved", "Rejected", "Pending", "Cancelled" etc...

There is even a way to get a "suggestion" from MySQL itself on how to restructure your table. When you do have a VARCHAR field, it can actually suggest you to change that column type to ENUM instead. This is done using the PROCEDURE ANALYSE() call.
