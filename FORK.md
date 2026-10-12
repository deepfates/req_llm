# This is agentjido/req_llm 1.25.0 plus one patch

Branch `patched-1.25.0` is upstream tag `v1.25.0` (its `lib/` and `mix.exs`
match the Hex 1.25.0 package) plus one commit per patch below. Dwell pins one
commit of this branch with `override: true`, because Imp asks for ReqLLM from
Hex.

To drop the pin: once an upstream release has every patch below, point Dwell
back at Hex at that version and delete this branch.

## The patches

| Commit subject | Needed by | Retires when |
| --- | --- | --- |
| feat(openrouter): support prompt_cache_key option | Dwell (OpenRouter models that cache per backend server) | upstream releases `openrouter_prompt_cache_key` (agentjido/req_llm PR, see below) |

**prompt_cache_key.** OpenRouter's documented `prompt_cache_key` request
field keeps calls that share a prompt prefix on one backend, so they read
each other's cache. ReqLLM 1.25.0 has no OpenRouter option that sends it and
refuses unknown provider options. The patch adds `openrouter_prompt_cache_key`,
sent the same way as `openrouter_session_id`. Test:
`test/providers/openrouter_test.exs` "encode_body OpenRouter-specific options"
fails on plain v1.25.0.
