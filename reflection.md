# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
**At first I didn't understand what is going on untill I open the developer Debug info. One thing shocked me was on my first attempt I got a negative score which it is an usually in games.**
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
1. **The hints were off, I would put o and still says "go lower" but the instructions is to choose number between 1 and 100**
2. **The ascore was negative and it will take even negative numbers**
---

## 2. How did you use AI as a teammate?

For this project I used AI tools such as GitHub Copilot in VS Code and ChatGPT. These tools helped me understand parts of the code and suggested possible fixes while I was debugging the game.

One example of a correct AI suggestion was when the AI suggested fixing the check_guess() function so that it returns only the outcome ("Win", "Too High", or "Too Low"). Originally, the function returned two values: the outcome and a message with emojis. However, the automated tests expected the function to return only a single string. After changing the function to return only the outcome, I verified the fix by running python -m pytest in the terminal. The tests then showed 3 passed, which confirmed that the function worked correctly with the test file.

One example of an incorrect or misleading suggestion was when the AI-generated code converted the secret number into a string on certain attempts (secret = str(st.session_state.secret)). This caused a bug when the program tried to compare the guessed number with the secret number using > or <. Since one value was an integer and the other was a string, Python produced a TypeError. I verified the issue by running the game and noticing the error message in the terminal. After identifying the problem, I fixed it by keeping the secret value as an integer at all times (secret = st.session_state.secret). Once this change was made, the game ran without the error.

---

## 3. Debugging and testing your fixes

To decide whether a bug was actually fixed, I tested the program both by running the Streamlit game and by running automated tests using pytest. If the game ran without crashing and the test cases passed, I considered the bug fixed.

One important test I ran was python -m pytest in the terminal. This ran the automated tests in the tests/test_game_logic.py file. At first, the tests failed because the check_guess() function returned two values instead of one. After modifying the function to return only the outcome string, I ran the tests again and saw the result 3 passed. This showed that the logic of the function matched what the tests expected.

AI tools also helped me understand the testing process. ChatGPT explained how to run pytest and how the tests were checking the return value of the check_guess() function. This helped me understand why the tests were failing and what change was needed to make them pass.

---

## 4. What did you learn about Streamlit and state?

- In the original app, the secret number kept changing unexpectedly because the code recalculated it during certain reruns, especially when the attempt number was even and the secret was converted to a string. This caused the secret to be inconsistent and also triggered type errors when comparing it to guesses. Streamlit “reruns” the script every time the user interacts with a widget, like clicking a button or entering a guess. To preserve values across reruns, Streamlit uses st.session_state, which allows variables such as the secret number, attempts, score, and history to persist between reruns. By storing the secret number in st.session_state and always keeping it as an integer, I was able to stabilize the game so that the secret number no longer changed unexpectedly.

---

## 5. Looking ahead: your developer habits

- One habit I want to reuse in future projects is testing iteratively with both automated tests and manual checks. Running pytest while also playing the game allowed me to quickly see whether my changes fixed the logic and whether the user experience worked as intended. One thing I would do differently next time is carefully review AI-generated suggestions before using them; while AI is helpful, it can suggest misleading or incorrect code that introduces subtle bugs. This project has made me realize that AI-generated code is a strong assistant, but it requires careful verification and understanding—AI can accelerate development, but developers still need to think critically about the results.
