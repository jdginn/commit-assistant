# commit-assistant

Small utility for suggesting git commit messages

This doesn't exist yet. But here are some ideas:

1. Write in go because it's portable and easy to work with
2. Pipe `git diff --cached` into an LLM and ask a few questions. For each question, ask the LLM to give a confidence score. Decide what to do next based on the scores.

- Is it possible this change is about multiple topics?
- If so, would you recommend splitting it into multiple commits?
- What is this change about?
- Come up with a first draft of your commit message.

3. Provide the last 10 commits

- Is this commit closely related to these previous commits?
- If so:
  - Does this commit look like it should be squashed with the previous commit?
  - Does this commit look like it should be squashed into an earlier commit?
  - If it shouldn't be squashed, should we change the commit message based on the relationship to the previous commits?

4. Provide output from a configured linter (optional)

- Look at these linter outputs. Do any of them look VERY important? Bias your answer toward saying "no".
- Do these linter outputs make you think we should change the commit message?

5. Provide the source of the modified files

- Do you see anything in these files that strongly suggests you should change the commit message?

6. Generate 5 options for the commit header

- User manually selects one of the 5

7. Generate 5 options for the commit body

- User manually selects one of the 5

8. Pipe the result into `git commit --edit -m`

Config:

- LLM model (only support local, start with ollama then maybe add llama.cpp)
  - Support two different models? A big and small one?
  - Support using a second model to check the first model's work?
- Optional stages:
  - Previous commits
  - Linter
    - Configure linter to use
  - File contents
-
