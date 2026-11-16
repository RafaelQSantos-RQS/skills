# LLMs.txt

LLM-optimized documentation endpoints for Optimus UI components.

## Agentskill-

The markdown files above are also bundled as an Agent Skill , the SKILL.md format supported by coding agents such as Claude Code, Codex, Cursor and OpenCode. Once installed, the agent reads the component docs, API tables and guides from disk whenever it works on Optimus UI code, instead of fetching them from this site each time. Install it with the skills CLI , which asks which agents to set it up for. By default the skill is installed into the current project, so your team gets it too. Add -g to install it for your user instead. You can also download the zip and extract it into a folder named optimus-ui in your agent's skills directory.

```bash
npx skills add https://optimus.openng.org

# update to the latest docs
npx skills update optimus-ui
```

## Llmsfulltxt-

The llms-full.txt file is a complete list of all the pages in the Optimus UI documentation. It is used to help AI models understand the entire documentation set.

## Llmstxt-

The llms.txt file is an industry standard that helps AI models better understand and navigate the Optimus UI documentation. It lists key pages in a structured format, making it easier for LLMs to retrieve relevant information.

## Markdownextension-

Add a .md to a page's URL to display a Markdown version of that page.

