---
name: weather-fetcher
description: Fetch current weather data from wttr.in API. Example skill demonstrating the skill format.
argument-hint: [city-name]
---

Fetch the current temperature for the specified city.

## Steps

1. Call `https://wttr.in/$ARGUMENTS?format=j1` using WebFetch
2. Extract the current temperature from the response
3. Report the temperature with the city name

## Example

`/weather-fetcher Stockholm` returns the current temperature in Stockholm.

## Why This Skill Exists

This is a minimal working example of a Claude Code skill.
Skills are preloaded knowledge injected into agents at startup.
They use YAML frontmatter for configuration and markdown for instructions.

Key fields:
- `name`: identifier for the skill
- `description`: tells Claude when to invoke it
- `argument-hint`: shows users what input to provide
