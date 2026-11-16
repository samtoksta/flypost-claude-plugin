# Flypost for Claude

Plan, write, design and schedule LinkedIn content with Claude, in your own voice and from your own
material. This plugin pairs the Flypost connector with skills that teach Claude how to use it well:
check new ideas against what you have already published, ground every claim in your Brain, follow
your writing voice, lay visuals out in your brand, and hand you the schedule card rather than
posting on its own.

You need a Flypost account. A 7-day free trial is available at [flypost.io](https://www.flypost.io).

## What's inside

**Connector.** The plugin connects Claude to Flypost's hosted MCP server at
`https://mcp.flypost.io/claude/mcp`, the same server as the Flypost listing in Claude's connector
directory. If you already have that connector, you keep one set of Flypost tools.

**Skills.** Claude loads each one when your request fits it:

| Skill | Use it when you ask Claude to... |
|---|---|
| `plan-post-ideas` | come up with post ideas, plan next week's content, or fill the idea board |
| `write-linkedin-post` | write or rewrite a LinkedIn post in your voice |
| `design-linkedin-visual` | turn an idea or post into a carousel, an infographic, or a stat or comparison image |
| `schedule-linkedin-post` | schedule, publish or cancel a post |

## Use it

1. Add the plugin, then connect Flypost from the plugin's **Connectors** tab and sign in.
2. Pick a project when Claude asks (or say "use my Flypost project").
3. Ask in plain words, for example:
   - "Give me five post ideas for next week that I haven't covered yet"
   - "Write a LinkedIn post about our pricing change, in my voice"
   - "Turn that into a 6-slide carousel in my brand"
   - "Schedule it for Tuesday at 9am"

Claude writes the words in the conversation and saves them to your Flypost account, where you and
your team can keep editing. It asks before it schedules, publishes, cancels or deletes anything.

## Data

The plugin contains only skills (Markdown) and the connector reference. It runs no scripts and
stores nothing itself. Everything Claude reads or saves goes between Claude and your Flypost
account through `mcp.flypost.io`, after you sign in with Flypost's own OAuth flow: your brand kit,
writing voice, Brain sources, ideas, drafts, designs, analytics and LinkedIn schedule. Posts reach
LinkedIn only when you schedule or publish them. This connection does not generate pictures with AI
image models.

Privacy policy: <https://www.flypost.io/privacy>. Help: <https://www.flypost.io/help/connect-flypost-to-chatgpt-or-claude>.
Support: hello@flypost.io.

## License

MIT. See [LICENSE](LICENSE).
