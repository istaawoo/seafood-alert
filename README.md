# Seafood Alert

A Java program that checks Purdue dining court menus every day and sends me a Telegram message when a seafood dish with no meat ingredients is being served.

## Project Goal

Seafood is one of the few proteins I can reliably eat in Purdue dining courts, but finding it means checking every menu by hand, and some seafood dishes (like shrimp prepared with chicken base or chicken fat) still contain meat. Seafood Alert automates the search and the ingredient check, then pings my phone.

## MVP Scope

- Pull each dining court's daily menu from the Purdue Dining API
- Detect seafood items using the Fish and Shellfish allergen tags
- Filter out items whose ingredients contain meat (chicken base, chicken fat, beef, pork, gelatin)
- Send a Telegram notification listing the item, dining court, and meal
- Track already notified items in `notified.txt` to avoid duplicate pings

## Future Plans (V2.0+)

- Weekly lookahead that pings for the whole upcoming week
- Integration into my existing personal food app
- Recommend the best time and location when multiple protein options exist
- User config file for custom keywords and favorite dining courts

## Tech Stack

| Area | Choice |
| --- | --- |
| Language | Java 17+ |
| HTTP | `java.net.http.HttpClient` |
| JSON parsing | Gson |
| Data source | Purdue Dining API (`api.hfs.purdue.edu/menus/v2`), public, no key |
| Notifications | Telegram Bot API (`sendMessage`) |
| Storage | `notified.txt` plain text file |
| Scheduling | cron, once every morning |

## Repo Structure

```
src/      Java source code
tests/    test cases
docs/     Eisenhower Matrix and system diagram (PNG + .drawio source)
```

## Build Plan

1. Set up repo, folder structure, and README
2. Fetch one dining court's menu and print the raw JSON
3. Parse the JSON with Gson and print every item by meal and station
4. Filter to items with Fish or Shellfish allergens
5. Fetch ingredients and remove anything containing meat
6. Loop through all dining courts and collect results
7. Create a Telegram bot and send a test message from Java
8. Send the filtered seafood list as a formatted Telegram message
9. Save notified items to `notified.txt` and skip duplicates
10. Schedule with cron and test a full daily run
