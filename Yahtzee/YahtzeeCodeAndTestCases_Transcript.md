# Yahtzee Code and Test Cases

Created: March 17, 2024 1:13 PM
Topic: Gen AI
Type: Assignment
Reviewed: Yes

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## I am trying to write a python code to build a bot that helps me play the game yahtzee. What are the functions I have to include here.

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here are some core functions you'll need for a Yahtzee helper bot in Python:

1. **Dice Rolling:**
    - `roll_dice(num_dice)`: This function simulates rolling a specified number of dice (usually 5) and returns a list of rolled values. You can use the `random` module to generate random numbers between 1 and سكانية (6).
2. **Score Calculation:**
    - `calculate_score(dice, category)`: This function takes the rolled dice (`dice` as a list) and a scoring category (`category` as a string like "full house") as input. It analyzes the dice and returns the score achieved for that specific category based on Yahtzee rules.
3. **Available Scores:**
    - `get_available_scores(dice)`: This function analyzes the rolled dice and returns a dictionary where keys are scoring category names and values are either `True` (if the category can be scored with the current roll) or `False`.
4. **Best Choice:**
    - `choose_best_move(dice, available_scores)`: This function is the core of your bot's decision-making. It takes the rolled dice and available scores as input and uses an algorithm to determine the category with the highest potential score. Here are some approaches:
        - Simple - Choose the category with the highest fixed score (e.g., Yahtzee, Full House).
        - Probabilistic - Analyze potential re-rolls and choose the category with the highest expected value based on probability of scoring different combinations.
5. **User Interaction (Optional):**
    - These functions would handle interaction with the user to display information and get user input:
        - `show_dice(dice)`: Display the rolled dice values.
        - `show_scores(available_scores)`: Display the available scoring categories and their potential scores.
        - `get_re_roll_choice(dice)`: Ask the user which dice they want to re-roll (if allowed in the specific Yahtzee variant).

Remember, this is a basic framework. You can add more functionalities like keeping track of score history, implementing different difficulty levels for the bot, or integrating with a Yahtzee game interface.

**share**

**more_vert**

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## Instead of get_available_scores(dice) can we do score(dice: list[int]) -> dict[str, int] which returns a dictionary containing what the yahtzee hand represented by the list dice would score in each Yahtzee category

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Absolutely, that's a great approach!  Having a single function to calculate all scores simplifies the logic and avoids redundancy. Here's a Python function named `score(dice)` that achieves what you described:

**Python**

`def score(dice: list[int]) -> dict[str, int]:
  """
  Calculates the score for each Yahtzee category for a given dice roll.

  Args:
      dice: A list of integers representing the rolled dice values (1-6).

  Returns:
      A dictionary where keys are Yahtzee category names (strings) and values are 
      corresponding scores (integers).
  """
  scores = {
      "ones": sum(die == 1 for die in dice),
      "twos": sum(die == 2 for die in dice),
      "threes": sum(die == 3 for die in dice),
      "fours": sum(die == 4 for die in dice),
      "fives": sum(die == 5 for die in dice),
      "sixes": sum(die == 6 for die in dice),
      "three_of_a_kind": sum(dice) if len(set(dice)) <= 3 else 0,
      "four_of_a_kind": sum(dice) if len(set(dice)) <= 2 else 0,
      "full_house": 25 if (len(set(dice)) == 2 and (2 in dice.count(dice[0]) or 3 in dice.count(dice[0]))) else 0,
      "small_straight": 30 if sorted(dice) == [1, 2, 3, 4] or sorted(dice) == [2, 3, 4, 5] else 0,
      "large_straight": 40 if sorted(dice) == [1, 2, 3, 4, 5] or sorted(dice) == [2, 3, 4, 5, 6] else 0,
      "yahtzee": 50 if all(dice.count(val) == 1 for val in dice) else 0,
      "chance": sum(dice),
  }
  return scores`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

This function takes a list of dice values (`dice`) and returns a dictionary (`scores`) containing all Yahtzee category names as keys and their corresponding scores for the given dice roll as values.

- It calculates the score for each category based on Yahtzee rules.
- It uses list comprehensions and set operations to efficiently identify dice combinations for categories like three-of-a-kind, four-of-a-kind, full house, straights, and Yahtzee.

By using this `score` function, you can easily determine the score for any category and integrate it into your Yahtzee helper bot's decision making logic.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## write the code for roll_dice

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here's the code for the `roll_dice` function in Python:

**Python**

`import random

def roll_dice(num_dice: int) -> list[int]:
  """
  Simulates rolling a specified number of dice.

  Args:
      num_dice: An integer representing the number of dice to roll.

  Returns:
      A list of integers representing the rolled dice values (1-6).
  """
  if num_dice <= 0:
    raise ValueError("Number of dice must be a positive integer.")

  return [random.randint(1, 6) for _ in range(num_dice)]`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

This function defines several aspects:

- **Import:** It imports the `random` module which provides functionalities for generating random numbers.
- **Function Definition:** It defines a function named `roll_dice` that takes an integer `num_dice` as input.
- **Docstring:** It includes a docstring explaining the function's purpose, arguments, and return value.
- **Input Validation:** It checks if `num_dice` is positive. If not, it raises a `ValueError`.
- **Random Dice Generation:** It uses list comprehension to create a list of `num_dice` random integers between 1 and 6 using `random.randint`.
- **Return Value:** It returns the generated list of dice values.

This code provides a basic implementation for rolling dice. You can further enhance it by adding functionalities like:

- Allowing users to specify different die types (e.g., 4-sided, 8-sided) by adding another argument to the function.
- Implementing re-rolls by taking another argument specifying the number of dice to re-roll after the initial roll.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## write a code for:calculate_score(dice, category)

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here's the code for the `calculate_score(dice, category)` function leveraging the previously defined `score` function:

**Python**

`def calculate_score(dice: list[int], category: str) -> int:
  """
  Calculates the score for a specific Yahtzee category for a given dice roll.

  Args:
      dice: A list of integers representing the rolled dice values (1-6).
      category: A string representing the Yahtzee category name.

  Returns:
      An integer representing the score for the specified category, 
      or 0 if the category is invalid.
  """
  scores = score(dice)
  if category in scores:
    return scores[category]
  else:
    return 0  # Invalid category`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

This function accomplishes the following:

- **Function Definition:** It defines a function named `calculate_score` that takes a list of dice values (`dice`) and a category name (`category`) as input.
- **Docstring:** It includes a docstring explaining the function's purpose, arguments, and return value.
- **Score Calculation:** It calls the previously defined `score` function to get a dictionary containing scores for all categories for the given dice roll.
- **Category Check:** It checks if the provided `category` exists as a key in the `scores` dictionary.
- **Valid Category:** If the category is valid, it returns the corresponding score from the `scores` dictionary.
- **Invalid Category:** If the category is invalid (not found in Yahtzee categories), it returns 0.

This approach leverages the `score` function to calculate scores for all categories efficiently and then retrieves the specific score based on the desired category.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## choose_best_move(dice, available_scores)

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here's a possible implementation for `choose_best_move(dice, available_scores)` with two approaches:

**1. Simple Approach (Choose Highest Fixed Score Category):**

**Python**

`def choose_best_move_simple(dice: list[int], available_scores: dict[str, bool]) -> str:
  """
  Chooses the best move (category) based on the highest fixed score 
  among available categories.

  Args:
      dice: A list of integers representing the rolled dice values (1-6).
      available_scores: A dictionary where keys are Yahtzee category names 
                         (strings) and values are True/False indicating 
                         availability.

  Returns:
      A string representing the Yahtzee category with the highest 
      fixed score (e.g., Yahtzee, Full House) among available categories.
  """
  best_score = 0
  best_category = None
  for category, available in available_scores.items():
    if available:
      category_score = calculate_score(dice, category)
      if category_score > best_score and category_score in (50, 40, 25):  # Fixed high-scoring categories
        best_score = category_score
        best_category = category
  return best_category or "re-roll"  # Return "re-roll" if no available category found`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

This approach iterates through the available categories and compares their scores (obtained using `calculate_score`) with a running `best_score`. It focuses on categories with fixed high scores (Yahtzee, Full House, Large Straight) to prioritize maximizing points.  If no available category offers a high fixed score, it returns "re-roll" to suggest re-rolling the dice.

**2. Probabilistic Approach (Considering Re-rolls):**

This approach is more complex and requires additional logic to analyze potential re-rolls and estimate expected values for categories. Here's a basic outline:

- Define functions to analyze dice combinations for potential re-rolls (e.g., how many dice could contribute to a specific category).
- Use simulations to estimate the expected score for each available category considering re-rolls and their probabilities.
- Choose the category with the highest expected score.

**Choosing the Best Approach:**

The simple approach is easier to implement but might not be optimal in all situations.  The probabilistic approach offers a potentially better strategy but requires more complex calculations. You can experiment with both approaches and see which works best for your bot's goals.

**Note:** This implementation assumes the `calculate_score` function is defined elsewhere.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## show_dice(dice)

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here's the code for `show_dice(dice)` that displays the rolled dice values in a user-friendly format:

**Python**

`def show_dice(dice: list[int]) -> None:
  """
  Displays the rolled dice values.

  Args:
      dice: A list of integers representing the rolled dice values (1-6).

  Returns:
      None
  """
  print("Rolled Dice:")
  for die in dice:
    print(f"[Die {dice.index(die)+1}] {die}")  # f-string for formatted output`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

This function defines several aspects:

- **Function Definition:** It defines a function named `show_dice` that takes a list of dice values (`dice`) as input.
- **Docstring:** It includes a docstring explaining the function's purpose, arguments, and return value (which is `None` since it only prints to the console).
- **Print Rolled Dice:** It prints a message "Rolled Dice:" to indicate the start of rolled dice values.
- **Iterate and Print:** It iterates through each die value in the `dice` list.
- **Formatted Output:** It uses an f-string to format the output, displaying "Die {index+1}" followed by the corresponding die value. This provides a clear association between the die number and its value.

This code provides a basic way to display the rolled dice. You can further customize it by adding features like:

- Different dice display symbols (e.g., pips, characters) depending on user preference.
- Colors for highlighting specific dice values.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## show_scores(available_scores)

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here's the code for `show_scores(available_scores)` that displays the available Yahtzee categories and their potential scores:

**Python**

`def show_scores(available_scores: dict[str, bool]) -> None:
  """
  Displays the available Yahtzee categories and their potential scores.

  Args:
      available_scores: A dictionary where keys are Yahtzee category names 
                         (strings) and values are True/False indicating 
                         availability.

  Returns:
      None
  """
  print("Available Categories:")
  for category, available in available_scores.items():
    if available:
      score = calculate_score(get_rolled_dice(), category)  # Assuming get_rolled_dice() exists
      print(f"{category}: {score} (Available)")
    else:
      print(f"{category}: Not Available")`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

This function incorporates the following functionalities:

- **Function Definition:** It defines a function named `show_scores` that takes a dictionary of available scores (`available_scores`) as input.
- **Docstring:** It includes a docstring explaining the function's purpose, arguments, and return value (which is `None` since it only prints to the console).
- **Print Available Categories:** It prints a message "Available Categories:" to indicate the list that follows.
- **Iterate and Print:** It iterates through each category and its availability in the `available_scores` dictionary.
- **Conditional Printing:**
    - If the category is available (True value), it calculates the score using `calculate_score` (assuming a function `get_rolled_dice` exists to retrieve the current dice roll) and prints the category name, score, and availability status.
    - If the category is not available (False value), it simply prints the category name and "Not Available" status.

**Note:** This code assumes the existence of a function `get_rolled_dice` that retrieves the current dice roll. You'll need to implement this function or integrate it with your Yahtzee game logic.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## write a fuction for keeping track of score history

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here's a function named `track_score_history(score, round_num)` that keeps track of the score history in your Yahtzee helper bot:

**Python**

`def track_score_history(score: int, round_num: int) -> None:
  """
  Keeps track of the score history for each round.

  Args:
      score: An integer representing the score achieved in the current round.
      round_num: An integer representing the current round number.

  Returns:
      None
  """
  # Implement logic to store score history (e.g., list, dictionary)
  # This example uses a list to store (round, score) tuples
  score_history.append((round_num, score))
  print(f"Round {round_num} Score: {score}")  # Print current round score`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

This function accomplishes the following:

- **Function Definition:** It defines a function named `track_score_history` that takes the current round's score (`score`) and round number (`round_num`) as input.
- **Docstring:** It includes a docstring explaining the function's purpose, arguments, and return value (which is `None` since it only updates the score history and prints the current score).
- **Score History Storage:** It requires implementing logic to store the score history. This example uses a global variable `score_history` (which needs to be declared outside the function) as a list to store tuples of (`round_num`, `score`). You can choose alternative data structures like dictionaries if you want to associate additional information with each round's score.
- **Append to History:** It appends a tuple containing the current round number and score to the `score_history` list.
- **Print Current Score:** It prints a message displaying the current round's score for user information.

**Additional Considerations:**

- You can modify the function to return the updated score history if needed for further analysis in your bot's logic.
- You can add functionalities to display the entire score history upon user request or after a certain number of rounds.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## write 25 test cases for this yahtzee game code

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

## **Yahtzee Helper Bot Test Cases (25)**

These test cases cover various functionalities of the Yahtzee helper bot code, including dice rolling, score calculation, available scores, best move selection, and score history tracking (assuming these functions are implemented).

**Dice Rolling (roll_dice):**

1. **Test Case 1:** Roll 5 dice, expect a list of 5 random integers between 1 and 6.
2. **Test Case 2:** Roll 0 dice, expect a ValueError for invalid input.
3. **Test Case 3:** Roll dice multiple times, verify different results each time (due to randomness).

**Score Calculation (calculate_score):**

1. **Test Case 4:** Calculate score for Yahtzee (all dice same value), expect 50.
2. **Test Case 5:** Calculate score for Full House (three of a kind and a pair), expect 25.
3. **Test Case 6:** Calculate score for Large Straight (1, 2, 3, 4, 5), expect 40.
4. **Test Case 7:** Calculate score for Three of a Kind (exactly three dice with same value), expect the sum of all dice.
5. **Test Case 8:** Calculate score for Fours of a Kind (exactly four dice with same value), expect the sum of all dice.
6. **Test Case 9:** Calculate score for categories requiring specific combinations (Small Straight, Chance), expect the correct sum based on dice values.
7. **Test Case 10:** Calculate score for a category not achievable with the dice roll (e.g., Yahtzee with non-matching dice), expect 0.
8. **Test Case 11:** Calculate score for an invalid category name, expect 0.

**Available Scores (get_available_scores):**

1. **Test Case 12:** Check available scores after a roll, expect categories achievable with the current dice to be marked True and others False.
2. **Test Case 13:** After using a category (e.g., Yahtzee), check if it becomes unavailable for subsequent rolls.

**Best Move Selection (choose_best_move):**

1. **Test Case 14:** Simulate a roll with Yahtzee (all dice same value), expect Yahtzee to be chosen as the best move (Simple Approach).
2. **Test Case 15:** Simulate a roll with potential for Full House and other categories, expect the best move to be chosen based on scoring strategy (Simple or Probabilistic Approach).
3. **Test Case 16:** Simulate a roll with no high-scoring categories available, expect "re-roll" to be suggested.

**Score History Tracking (track_score_history):**

1. **Test Case 17:** Track score for the first round, verify it's stored correctly in the score history.
2. **Test Case 18:** Track scores for multiple rounds, verify each round's score is added to the history.
3. **Test Case 19:** Optionally, test retrieving the entire score history or specific round information.

**Integration and User Interaction:**

1. **Test Case 20:** Simulate a Yahtzee game turn, integrating dice rolling, score calculation, best move suggestion, and score history tracking.
2. **Test Case 21:** Test displaying rolled dice values using the show_dice function (assuming implemented).
3. **Test Case 22:** Test displaying available categories and potential scores using the show_scores function (assuming implemented).

**Error Handling:**

1. **Test Case 23:** Test handling of invalid user input for number of dice to roll (negative value).
2. **Test Case 24:** Test handling of errors during score calculation due to unexpected data types or logic issues.

**Additional Considerations:**

1. **Test Case 25:** Consider testing the bot's performance and decision-making over multiple simulated games to evaluate its effectiveness.

These test cases provide a starting point for ensuring the functionality and robustness of your Yahtzee helper bot code. You can further expand these tests based on specific features and functionalities you implement.

[https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c](https://lh3.googleusercontent.com/a/ACg8ocLNt_XwTfKflACtwChRCpUWS1Njc7-o-H9fiRfm5_tKyx0=s64-c)

## write the code to execute: **Dice Rolling (roll_dice):**
1. **Test Case 1:** Roll 5 dice, expect a list of 5 random integers between 1 and 6.
2. **Test Case 2:** Roll 0 dice, expect a ValueError for invalid input.
3. **Test Case 3:** Roll dice multiple times, verify different results each time (due to randomness).
in a colab notebook

![https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg](https://www.gstatic.com/lamda/images/gemini_sparkle_v002_d4735304ff6292a690345.svg)

Here's the Colab notebook code to execute the first 3 test cases for dice rolling:

**Python**

`import unittest
import random

# Define the roll_dice function (assuming it's not already defined elsewhere)
def roll_dice(num_dice):
  """
  Simulates rolling a specified number of dice.

  Args:
      num_dice: An integer representing the number of dice to roll.

  Returns:
      A list of integers representing the rolled dice values (1-6).
  """
  if num_dice <= 0:
    raise ValueError("Number of dice must be a positive integer.")

  return [random.randint(1, 6) for _ in range(num_dice)]

# Test Cases (adapted as functions for easier execution)
def test_roll_dice_5():
  """Test rolling 5 dice, expect a list of 5 random integers between 1 and 6."""
  rolled_dice = roll_dice(5)
  if len(rolled_dice) != 5:
    print("Error: Incorrect number of dice rolled.")
    return
  for die in rolled_dice:
    if not (1 <= die <= 6):
      print("Error: Die value outside valid range (1-6).")
      return
  print("Test Passed: Roll_dice(5) returned a valid list of 5 dice values.")

def test_roll_dice_0():
  """Test rolling 0 dice, expect a ValueError for invalid input."""
  try:
    roll_dice(0)
  except ValueError as e:
    print("Test Passed: Roll_dice(0) raised a ValueError:", e)
  else:
    print("Error: Roll_dice(0) did not raise a ValueError.")

def test_roll_dice_multiple():
  """Test rolling dice multiple times, verify different results."""
  rolls = [roll_dice(5) for _ in range(3)]
  if rolls[0] == rolls[1]:
    print("Error: Consecutive rolls produced identical results.")
  elif rolls[1] == rolls[2]:
    print("Error: Consecutive rolls produced identical results.")
  else:
    print("Test Passed: Multiple rolls produced different results.")

# Execute Test Cases
test_roll_dice_5()
test_roll_dice_0()
test_roll_dice_multiple()`

**Use code [with caution.](https://gemini.google.com/faq#coding)content_copy**

**Explanation:**

1. We import `unittest` and `random` for testing and dice rolling.
2. We define the `roll_dice` function (assuming it's not already defined).
3. We define separate functions for each test case (`test_roll_dice_5`, `test_roll_dice_0`, `test_roll_dice_multiple`).
    - These functions perform the tests and print messages indicating success or failure.
4. We call each test case function to execute them in the notebook.

**Note:**

- This approach uses functions to organize the test cases for better readability.
- You can adapt this structure to write test cases for other functionalities of your Yahtzee helper code.