# Billing

Billing is done on a per-token basis. Inputs are tokenized using the OpenAI-Gpt3.5 token specification, and you are charged $1/million tokens input. **There is no charge for output tokens.**

## Minimum Billing

In some cases, your contexts will be too small to do any meaningful prompt compression. This most often happens with prompts under 1000 characters. In this case, you are billed for 100 tokens i.e 'The minimum bill rate'.  

When this occurs, a `-1` value is returned in the `tokensCharged` field to indicate the minimum bill rate was applied.
