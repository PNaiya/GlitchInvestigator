# 💭 Reflection: Game Glitch Investigator  
---

## **1. What was broken when you started?**

When I first ran the game, the UI loaded correctly, but the gameplay behavior was inconsistent. The most noticeable issue was that the hint system was unreliable — sometimes a guess that was clearly lower than the secret number produced a “Too high” message. I also noticed that the score counter behaved strangely, occasionally decreasing twice or not updating at all. In one run, the game didn’t end even after I guessed the correct number, which suggested a logic issue in how the win condition was handled. These bugs made it clear that both the hint logic and the game flow needed investigation.

---

## **2. How did you use AI as a teammate?**

I used GitHub Copilot inside VS Code as my main AI assistant, and I also used Copilot Chat for deeper explanations of the logic. One correct suggestion Copilot gave was to move the `check_guess` function out of `app.py` and into `logic_utils.py` to separate UI from logic. After applying this refactor, I verified the change by running pytest and confirming that the logic behaved consistently in the Streamlit app.  

One misleading suggestion Copilot gave was to rewrite the entire scoring system using a more complex state object. The diff it generated touched multiple files unnecessarily and introduced new bugs. I caught this by reviewing the diff carefully and noticing that the logic no longer matched the game’s intended behavior. I discarded the suggestion and instead asked Copilot for a smaller, targeted fix, which worked correctly.

---

## **3. Debugging and testing your fixes**

To decide whether a bug was truly fixed, I combined automated tests with manual gameplay. After fixing the hint logic, I wrote a pytest test that checked whether a guess of 60 against a secret of 50 returned “Too high.” The test passed, and when I ran the game manually, the hints matched my expectations across multiple guesses.  

AI helped me design the test by suggesting a simple structure for verifying the output of `check_guess`. Copilot also helped me understand how to isolate the logic so the test didn’t depend on Streamlit’s UI state. This combination of automated and manual testing gave me confidence that the fix was stable.

---

## **4. What did you learn about Streamlit and state?**

Streamlit reruns the entire script from top to bottom every time a user interacts with the app, which can be surprising if you’re used to traditional web frameworks. To keep values from resetting on every rerun, Streamlit uses `st.session_state`, which acts like a small dictionary that survives between reruns. I would explain it to a friend like this: “Streamlit refreshes constantly, so session state is where you store anything you don’t want to lose — like the secret number, the score, or whether the game is over.”

---

## **5. Looking ahead: your developer habits**

One habit I want to reuse is writing a small test immediately after fixing a bug. It forced me to think clearly about what the function should do and gave me a reliable way to confirm the fix. Another habit I want to keep is reviewing Copilot’s diffs carefully instead of accepting large changes automatically.  

Next time I work with AI on a coding task, I’ll be more specific in my prompts so the AI focuses on the smallest possible change instead of rewriting entire sections. This project showed me that AI‑generated code can be helpful, but it still needs human judgment — especially when debugging or refactoring logic.
