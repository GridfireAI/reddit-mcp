# Reddit MCP

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A plug-and-play [MCP](https://modelcontextprotocol.io) server to browse, search, and read Reddit.

<a href="https://glama.ai/mcp/servers/@GridfireAI/reddit-mcp">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@GridfireAI/reddit-mcp/badge" alt="Reddit MCP server" />
</a>

## Demo
Here's a short video showing how to use this in Claude Desktop:

https://github.com/user-attachments/assets/a2e9f2dd-a9ac-453f-acd9-1791380ebdad

## Features

- Detailed parameter validation with [pydantic](https://docs.pydantic.dev)
- Uses the reliable [PRAW](https://praw.readthedocs.io/) library under the hood
- Built-in rate limiting protection thanks to PRAW

## Caveats
- Only supports read features for now. If you want to use write features, upvote the [issue](https://github.com/GridfireAI/reddit-mcp/issues/1) or [send a PR](CONTRIBUTING.md)! 🙌
- Tools use tokens. To use this with Claude, you may need to be a Pro user to use many tool calls. Free tier users should be fine with lighter tool usage. Your token usage is your responsibility.

## Installation

### Prerequisite: Reddit API credentials

Create a [developer app](https://www.reddit.com/prefs/apps) in your Reddit account if you don't already have one. This will give you a `client_id` and `client_secret` to use in the following steps. If you already have these, you can skip this step.

### Claude Desktop

To install into Claude Desktop:

- Follow the instructions [here](https://modelcontextprotocol.io/quickstart/user) until the section "Open up the configuration file in any text editor."
- Add the following to the file depending on your preferred installation method:

### Using [uvx](https://docs.astral.sh/uv/guides/tools/) (recommended)

```json
"mcpServers": {
  "reddit": {
    "command": "uvx",
    "args": ["reddit-mcp"],
    "env": {
      "REDDIT_CLIENT_ID": "<client_id>",
      "REDDIT_CLIENT_SECRET": "<client_secret>"
    }
  }
}
```

### Using PIP

First install the package:

```bash
pip install reddit-mcp
```

Then add the following to the configuration file:

```json
"mcpServers": {
  "reddit": {
    "command": "python",
    "args": ["-m", "reddit_mcp"],
    "env": {
      "REDDIT_CLIENT_ID": "<client_id>",
      "REDDIT_CLIENT_SECRET": "<client_secret>"
    }
  }
}
```

### Others

You can use this server with any [MCP client](https://modelcontextprotocol.io/docs/clients), including agent frameworks (LangChain, LlamaIndex, AutoGen, etc). For an example AutoGen integration, check out the [example](examples/autogen).

## Tools

The tools the server will expose are:

| Name                         | Description                              |
| ---------------------------- | ---------------------------------------- |
| `get_comment`                | Access a comment                         |
| `get_comments_by_submission` | Access comments of a submission          |
| `get_submission`             | Access a submission                      |
| `get_subreddit`              | Access a subreddit by name               |
| `search_posts`               | Search posts in a subreddit              |
| `search_subreddits`          | Search subreddits by name or description |

## Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for more information.

## Acknowledgments

- [PRAW](https://praw.readthedocs.io/) for an amazingly reliable library 💙