# Format Telegram Post with Bitly Links

Format a Telegram post by automatically inserting relevant bit.ly links from the database.

## Input

The user will provide a Telegram post text as argument: $ARGUMENTS

## Instructions

1. Read the bitly links database from `.claude/commands/_data/bitly_links.json`

2. Analyze the input text and find opportunities to insert links based on:
   - **Keywords matching**: Look for mentions of terms that correspond to link descriptions
   - **Context matching**: Understand what the text is about and suggest relevant links

3. **Matching approach**:
   - Read all links from the database with their `description` fields
   - Use your judgment to find phrases in the post text that semantically match any link's purpose
   - Consider context, synonyms, and related concepts - not just exact keyword matches
   - The `description` field in each link entry explains what that link is for

4. **Output format**:

   Output the text in **raw Markdown format** inside a code block:
   - Use `[text](bitly_url)` format for links
   - Wrap the entire formatted post in triple backticks (```) so the terminal displays raw Markdown without rendering
   - This allows the user to see exactly where links are placed and copy the text easily
   - Don't over-link - max 3-5 links per post unless post is very long
   - Prioritize the most relevant links

5. **Output structure**:

   First show the formatted post inside a code block:

   ~~~
   ```
   [The post text with Markdown links like [word](https://bit.ly/xxx)]
   ```
   ~~~

   Then show the links summary table (outside code block):

   ```
   ## Links Used

   | Link text | Bitly | Description |
   |-----------|-------|-------------|
   | text | url | what it links to |

   ## Notes (if any)

   - Any suggestions or observations
   ```

## Example

**Input:**
```
Напоминаю, что первые 12 месяцев у вас скидка на Seguridad Social. Подробности в документе.
```

**Output:**

## Formatted Post

~~~
```
Напоминаю, что первые 12 месяцев у вас [скидка на Seguridad Social](https://bit.ly/ss-tarifa-plana-loose-risk). Подробности в [документе](https://bit.ly/autonomo-manual).
```
~~~

## Links Used

| Link text | Bitly | Description |
|-----------|-------|-------------|
| скидка на Seguridad Social | bit.ly/ss-tarifa-plana-loose-risk | Риск лишиться скидки Seguridad Social |
| документе | bit.ly/autonomo-manual | Main document - Russian version |

## Important Notes

- Telegram channel is in Russian - only use links that lead to the Russian version of the site (check `expected_url` field in the database - should contain `/ru/` or lead to an external service)
- Don't add links to phrases that already have links
- Keep link anchors short and natural - prefer single words or 2-3 word phrases
- If no relevant links found, say so and return the original text unchanged
