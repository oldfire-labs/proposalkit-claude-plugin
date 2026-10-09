# Evals

Each case is one request a user might type. The `b*` cases ask for a proposal
without naming ProposalKit, the `c*` cases also ask for something plain text
can't give (a hosted link, branding from a site, open tracking), and the `n*`
cases are proposals the skill should leave alone. Every case grades one thing:
whether Claude called `create_proposal`.

The ProposalKit tools are mocked from `mocks/proposalkit/`, so runs never
touch the live API. Tool descriptions shape whether Claude picks a tool, so
before a run, save the `result` of a `tools/list` request to the ProposalKit
MCP server as `mocks/proposalkit/_tools.json`. The file is gitignored, and
without it the mocks use placeholder schemas.

The question is what the skill adds over the connector alone, so compare two
arms by path rather than with `--ablation` (which drops the connector too):

```bash
claude plugin eval . --ablation none --model claude-opus-5-5
```

The connector-only arm is a copy of the plugin without `skills/`:

```bash
mkdir -p /tmp/pk-connector-only/.claude-plugin && cp .claude-plugin/plugin.json /tmp/pk-connector-only/.claude-plugin/ && cp .mcp.json /tmp/pk-connector-only/ && cp -R evals /tmp/pk-connector-only/
```

```bash
claude plugin eval /tmp/pk-connector-only --ablation none --model claude-opus-5-5
```
