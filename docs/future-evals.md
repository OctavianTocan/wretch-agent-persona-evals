# Future Evals

The current harness is intentionally small. Useful next steps, in order of
value, would be:

1. Full-suite scheduled smoke

   Run all 12 cases on a timer and alert on failures. This catches obvious
   persona regressions quickly.

2. Multi-turn correction evals

   Test whether Wretch recovers after being told the answer was wrong, instead
   of resending or defending the previous answer.

3. Tool-boundary evals

   Feed prompts that ask for edits, pushes, public posts, restarts, deletions,
   and image generation. Verify Wretch asks for approval or scopes the action
   correctly.

4. Live-agent path evals

   Route through the real Wretch OpenClaw agent instead of the direct model
   prompt. This would test model behavior plus runtime state, tool availability,
   prompt assembly, memory, and session handling.

5. Telegram-visible evals

   Send synthetic prompts through the same user-visible channel that a person
   sees. This catches formatting, duplicate sends, delivery-account mistakes,
   and response-shape problems that direct model calls miss.

6. Cross-agent privacy evals

   Verify Wretch refuses to inspect or summarize another agent's private session
   data unless the user has explicitly authorized a narrow operational audit.

7. Pairwise persona comparison

   Compare Wretch against a generic assistant baseline and ask the judge which
   answer is more Wretch-like. Pairwise judging is often easier than absolute
   scoring.

8. Judge calibration set

   Add a small set of human-labeled good and bad responses. The judge should
   pass the calibration set before its scores are trusted.

9. Different judge model

   Keep Gemini 3 Flash as the candidate if desired, but use a different judge
   family for less self-agreement. A stronger judge is useful for subtler tone
   and boundary failures.

10. Regression archive

   Store sanitized examples of failed responses with the fix that followed.
   Over time, this becomes a local dataset of failures that actually mattered.
