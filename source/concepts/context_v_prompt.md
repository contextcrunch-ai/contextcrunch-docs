# Context & Prompt

For prompt compression, the prompt is typically divided into two parts: a compressible (context) part, and a non-compressible (prompt) part. ContextCrunch uses the prompt to trim off redundant information from the context.

## The Context

The context is the information that is less sensitive to information loss, and more suited for compression. In other words, not _all_ of the information in the context is strictly necessary to answer the user's query.

### Context Examples

- A Long conversation history.
- The complete text of textbook.
- A knowledgebase about a company.

## The Prompt

The prompt indicates the specific information that the user is looking for. This part is more sensitive to compression, since cutting out any portion of the prompt may siginificantly change what the LLM understands the task to be. ContextCrunch does not compress the prompt.

The prompt is used to infer which information from the context should be kept.

### Prompt Examples

- The most recent message from the user: `User: "Can You repeat the question?"`.
- A query about the context: `"How many flowers did lucie pick?"`.
- A specific task: `"Find all products that cost more than $5"`.
