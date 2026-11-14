# PRAXO-CORE for Erlang

PRAXO-CORE is an embeddable, MIT-licensed agent framework. This package is its native Erlang Core with source tag `erlang/v0.7.1`. It passes all eleven shared vector groups on Erlang/OTP 29 and includes the native agent loop, memory store, checkpoint allowlist, lexical path policy, context compaction, event sinks, middleware helpers, tool selection, and human-in-the-loop interrupt decisions. It does not call Go or another Core.

## At a glance

| Field | Value |
| --- | --- |
| Package | `praxo_core_erlang` |
| Registry | [Hex](https://hex.pm/packages/praxo_core_erlang/0.7.1) |
| Install | `{praxo_core, "0.7.1", {pkg, praxo_core_erlang}}` |
| Source version | `0.7.1` |
| Published version | `0.7.1` |
| Source tag | `erlang/v0.7.1` |
| Tier | Core |
| Contract | `SPEC_VERSION` `0.2.0` |
| Documentation | https://axisvela.github.io/praxo-core/languages/erlang/ |
| License | MIT |

## Highlights

- Hex package name: `praxo_core_erlang`; OTP application name: `praxo_core`.

## Quick start

Install the published package:

```erlang
{praxo_core, "0.7.1", {pkg, praxo_core_erlang}}
```

```erlang
Model = praxo_agent:static_model(<<"hello">>),
Options = praxo_agent:new_agent_options(Model),
{ok, Result, _Options} =
    praxo_agent:run_agent(Options, praxo_models:session(<<"demo">>), <<"hello">>),
io:format("~s~n", [maps:get(output, Result)]).
```

See the [full Erlang README](language/erlang/README.md) for complete installation, build, and verification commands.

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native | `praxo_openai_compatible` |
| Anthropic model | native | `praxo_anthropic` |
| Gemini model | native | `praxo_gemini` |
| MCP client | native | `praxo_mcp`; stdio, plus `praxo_mcp_http:transport/2` for Streamable HTTP 2025-03-26 |
| Harmovela sink | native | `praxo_harmovela` |
| OpenTelemetry sink | native (transport seam) | `praxo_otel`; caller supplies transport |
| Subagent delegation | native (synchronous seam) | `praxo_delegation:subagent_run/2`; no asynchronous manager |
| Retriever | native | `praxo_retriever:document`, `func_retriever`, `retrieve/3` |

## Examples

Runnable examples live under [`language/erlang/examples`](language/erlang/examples).

| Example | What it shows |
| --- | --- |
| [checkpoint](language/erlang/examples/checkpoint) | This example uses the Erlang Core checkpoint allowlist to encode and decode only registered payload types. |
| [event-sink](language/erlang/examples/event-sink) | This example uses the Erlang Core sink composition to fan out lifecycle and tool events and filter the tool-only stream. |
| [identity-policy](language/erlang/examples/identity-policy) | This example binds a trusted principal to policy decisions and rejects missing, inactive, role-mismatched, and tenant-mismatched actions. |
| [mcp](language/erlang/examples/mcp) | This example uses a caller-owned in-process transport with the Erlang MCP client. It covers initialize, `tools/list`, and `tools/call` without a server process. |
| [provider-fallback](language/erlang/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary failure when both fail. |
| [retry](language/erlang/examples/retry) | This example retries a transient failure with a bounded attempt count and keeps the exhausted failure state. |
| [service](language/erlang/examples/service) | This example defines a transport-neutral request handler boundary with health, principal, and run cases. Wire it into any Erlang HTTP server. |
| [streaming](language/erlang/examples/streaming) | This example collects agent stream parts from the Erlang Core and checks the `values` and `messages` lifecycle. |
| [structured-output](language/erlang/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Verify

Run the checks from `language/erlang`:

```bash
python language/erlang/run-tests.py
python language/erlang/api-snapshot.py --check
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/erlang/README.md`](language/erlang/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>

## Repository layout

- `language/erlang/` — implementation source, tests, API snapshot, and examples
- `spec/` — shared contract, vectors, and parity inventories
- `LICENSE` — MIT license

## Canonical source

- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/erlang
- Registry introduction: `language/erlang/REGISTRY.md`
- Machine-readable entry: `language/erlang/llms.txt` and `language/erlang/llms.md`
- Mirror repository: https://github.com/axisvela/praxo-core-erlang
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical Erlang source. The monorepo remains the source of truth and the release workflow source.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

MIT licensed.
