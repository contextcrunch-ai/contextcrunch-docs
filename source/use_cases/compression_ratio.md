# Compression Ratio

The `compression_ratio` parameter determines how much compression is applied to your context. The corresponds to the target percentage of the original (context + prompt) tokens are retained in the output.

## Example

Say we have the context:
Context: `A student is studying the effects of sunlight on plant growth for a science project.` (16 tokens)
Prompt: `What is the student studying?` (6 tokens)

The total number of tokens is 16 + 6 = 22. With a compression ratio of 0.9, we would expect an output of (1-0.9)*22 = ~ 2 tokens.

Notice that in this case, the compressed context + prompt would need to be smaller than the prompt itself.

## Best Practises

In general, you want to ensure `prompt_tokens > context_tokens*(1-compression ratio)` in order to ensure that, at the very least, the prompt can be returned. Generally, ContextCrunch will detect when violations of this constraint, and return the whole context, along with a `-1` in the `tokensCharged` field, indicating that compression could not be performed.

Additionally, as a rule of thumb, you also want to ensure that the overall `prompt_tokens + context_tokens` is at least 300 tokens, otherwise, again, compression my fail, since there is just not enough information in the context to compress.
