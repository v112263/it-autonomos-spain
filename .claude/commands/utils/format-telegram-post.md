# Format Telegram Post with Bitly Links

Format a Telegram post by automatically inserting relevant bit.ly links from the database.

## Input

The user will provide a Telegram post text as argument: $ARGUMENTS

## Instructions

1. Read the bitly links database from `.claude/commands/_data/bitly_links.json`

2. **Normalize line breaks**:
   - Remove line breaks **within sentences** (merge broken sentences into single lines)
   - Keep line breaks **between sentences** within the same paragraph (single line break after sentence-ending punctuation)
   - Keep paragraph separators (double line breaks / empty lines between paragraphs)
   - In other words: if a sentence is split across multiple lines, merge it; but don't merge separate sentences

3. **Convert formatting to Telegram-compatible syntax**:
   - Telegram uses its own markdown variant, convert if needed:
     - **Bold**: `**text**` (double asterisks)
     - **Italic**: `__text__` (double underscores) - NOT single asterisks!
     - **Bold + Italic**: `**__text__**`
     - **Strikethrough**: `~~text~~`
   - If input uses `*text*` for italic, convert to `__text__`
   - If input uses `_text_` for italic, convert to `__text__`

4. **Handle existing links in the input text**:
   - If the text already contains Markdown links `[text](url)`, check each URL:
     - **Bitly links** (`bit.ly/*`): Keep them as-is
     - **Non-bitly links**: Check if a matching bit.ly link exists in the database (compare `expected_url` field). If found, replace the URL with the corresponding bit.ly link
   - This ensures all links use bit.ly for tracking purposes

5. Analyze the input text and find opportunities to insert **additional** links based on:
   - **Keywords matching**: Look for mentions of terms that correspond to link descriptions
   - **Context matching**: Understand what the text is about and suggest relevant links

6. **Matching approach**:
   - Read all links from the database with their `description` fields
   - Use your judgment to find phrases in the post text that semantically match any link's purpose
   - Consider context, synonyms, and related concepts - not just exact keyword matches
   - The `description` field in each link entry explains what that link is for

7. **Output format**:

   Output the text in **raw Markdown format** inside a code block:
   - Use `[text](bitly_url)` format for links
   - Wrap the entire formatted post in triple backticks (```) so the terminal displays raw Markdown without rendering
   - This allows the user to see exactly where links are placed and copy the text easily
   - Don't over-link - max 3-5 links per post unless post is very long
   - Prioritize the most relevant links

8. **Output structure**:

   First show the formatted post inside a code block:

   ~~~
   ```
   [The post text with Markdown links like [word](https://bit.ly/xxx)]
   ```
   ~~~

   Then show the links summary table (outside code block):

   ```
   ## Links Replaced (if any)

   | Original URL | Replaced with | Description |
   |--------------|---------------|-------------|
   | original url | bit.ly/xxx | what it links to |

   ## Links Added

   | Link text | Bitly | Description |
   |-----------|-------|-------------|
   | text | url | what it links to |

   ## Notes (if any)

   - Any suggestions or observations
   ```

9. **Save to file**:
   - Save **only the formatted post text** to a file (no headers, no code block markers, no tables)
   - Just the raw text with Telegram markdown formatting and links, ready to copy-paste
   - File path: `.claude/commands/utils/telegram-post-YYYY-MM-DD-HH-MM-SS.txt`
   - Use current date and time for the filename
   - Display the file path to the user after saving

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

## Links Replaced

_No links replaced_

## Links Added

| Link text | Bitly | Description |
|-----------|-------|-------------|
| скидка на Seguridad Social | bit.ly/ss-tarifa-plana-loose-risk | Риск лишиться скидки Seguridad Social |
| документе | bit.ly/autonomo-manual | Main document - Russian version |

## Important Notes

- Telegram channel is in Russian - only use links that lead to the Russian version of the site (check `expected_url` field in the database - should contain `/ru/` or lead to an external service)
- Don't add links to phrases that already have links
- Keep link anchors short and natural - prefer single words or 2-3 word phrases
- If no relevant links found, say so and return the original text unchanged
