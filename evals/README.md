# Evals

Each case is one request a user might type. The `b*` cases ask for a proposal
without naming ProposalKit, the `c*` cases also ask for something plain text
can't give (a hosted link, branding from a site, open tracking), and the `n*`
cases are proposals the skill should leave alone. Every case grades one thing:
whether Claude called `create_proposal`.

The ProposalKit tools are mocked from `mocks/proposalkit/`, so runs never
touch the live API. Tool descriptions shape whether Claude picks a tool, so
save the server's real tool list next to the mocks before a run (it's
gitignored; without it the mocks use placeholder schemas):

```bash
curl -s https://api.proposalkit.io/mcp -H 'content-type: application/json' -H 'accept: application/json, text/event-stream' -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}' | jq '{tools: [.result.tools[] | del(._meta)]}' > evals/mocks/proposalkit/_tools.json
```

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
