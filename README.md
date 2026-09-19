# AI Debugging Assistant

Task Objective 
Write a natural-language prompt that will be given to an AI assistant (like ChatGPT). The AI will use your prompt to:
- Analyze a student’s buggy Python code
- Offer helpful suggestions or hints
- Avoid giving away the correct solution


## The single prompt
(Provided as a separate file: `prompt.txt`)


## Brief explanation of design choices

Why I worded it this way

- Explicit role & constraints: I open by assigning a clear role (Debugging Assistant) and a strict constraint (no full solution). This focuses the model on pedagogy and diagnostic guidance rather than generating fixes.
  
- Structured output: A fixed output template (Summary → Diagnostics → Likely cause → Hint → Tests) makes responses predictable, concise, and easy for graders to evaluate.
  
- Diagnostic-first flow: The prompt asks for concrete diagnostic steps before any hypothesis. This enforces the scientific testing approach (observe → test → infer), which both mirrors how engineers debug and teaches the student good habits.
  
- Minimal hints, not fixes: Hints are limited to tiny pseudocode sketches — enough to guide thought but not to copy/paste into a solution. This satisfies the requirement to avoid revealing the correct solution.
  
- Requesting minimal reproducible context: The assistant asks for the smallest missing piece of evidence (traceback, failing test, or minimal snippet) to reduce back-and-forth and increase accuracy.

How the prompt prevents giving the solution
- Multiple explicit instructions forbid returning corrected code blocks or exact line-by-line replacements.
- Hints are constrained to short pseudocode sketches and conceptual explanations only.
- The assistant must refuse explicit requests for the full solution and instead offer progressive hints and a verification checklist.

How the prompt encourages helpful, student-friendly feedback
- The assistant is asked to use a Socratic, friendly tone and to suggest 2–4 small, testable diagnostics. This motivates learning through experimentation.
- Each diagnostic must include how to run it and how to interpret results, teaching students not only *what* to try but *why*.



## Reasoning 

1. What tone and style should the AI use when responding?
Friendly, patient, Socratic tutor style. Use short sentences, ask guiding questions, avoid judgement, and encourage small experiments. Focus on clarity and actionable steps rather than long lectures.

2. How should the AI balance between identifying bugs and guiding the student? 
First concentrate on narrowing the problem by summarizing the evidence. Then propose concrete diagnostics (tests or prints) to isolate the fault. Only after tests are observed should the assistant suggest the likely cause and provide minimal hints. This ensures the AI guides the student to *discover* the bug rather than handing them the fix.

3. How would you adapt this prompt for beginner vs. advanced learners?
- Beginner: Add short conceptual reminders (e.g., “Remember: Python lists are 0-indexed”), more detailed interpretation of diagnostics, and slightly longer pseudocode hints. Provide 1–2 example unit tests to run.
  
- Advanced: Reduce scaffolding; request targeted unit tests, edge-case generation, or complexity checks. Hints become briefer and assume familiarity with debugging tools (e.g., using a debugger, `pytest`, or `hypothesis`).


