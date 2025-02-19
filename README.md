# SW_Challenge

# Unlock the Rebel Code Challenge

Welcome to the Unlock the Rebel Code challenge! In this exercise, you will build a serverless application that interacts with the [Star Wars API (SWAPI)](https://swapi.dev/documentation#intro) to generate a secret Rebel code. This challenge is designed to test your skills in Python, AWS Lambda, AWS Step Functions, microservices, and API integrations.

---

## Overview

Your goal is to build a solution that:

- **Retrieves data** from SWAPI endpoints.
- **Processes the data** through a multi-step workflow.
- **Generates a secret code** based on the processed data.
- **Exposes the solution** via an API Gateway endpoint.

The secret code is generated by combining parts of the data from a selected film and a planet. For example, using the film’s episode ID (mapped to a letter), a digit derived from a planet attribute, and the first letter of the planet’s name.

---

## Technical Requirements

### Architecture

- **AWS Lambda:**  
  Write your functions in Python.
  
- **AWS Step Functions:**  
  Orchestrate your Lambda functions into a workflow.

- **API Gateway:**  
  Expose your solution via a REST endpoint that triggers the Step Functions workflow.

### Data Flow and Logic

1. **Film Selection:**
   - Query the `/films/` endpoint from SWAPI.
   - Choose the film with the **earliest release date** (e.g., "A New Hope").
   - Extract the film’s `episode_id` and the list of character URLs.

2. **Character Processing:**
   - For each character URL from the selected film, query the `/people/` endpoint.
   - Extract a numeric attribute from each character (for example, `height`).
   - Compute an aggregate value (e.g., the **average height** of all characters).

3. **Planet Selection:**
   - Retrieve a list of planets from the `/planets/` endpoint.
   - Use the computed aggregate (e.g., average height, rounded to an integer) to select one planet.  
     *Hint:* Use modulo arithmetic if the value is larger than the number of available planets.
   - Extract details of the chosen planet (its name, residents, or population).

4. **Secret Code Generation:**
   - **Film Mapping:**  
     Convert the film’s `episode_id` to a letter (e.g., 1 → A, 2 → B, …, 4 → D).
   - **Planet Mapping:**  
     - Use the first letter of the planet’s name (e.g., Tatooine → T).
     - Derive a digit from a planet attribute. For example, use the length of the `"residents"` array (or apply a transformation to the `"population"` attribute, such as modulo 10).
   - **Assembly:**  
     Concatenate these elements (letter, digit, letter) to form the final secret code.

---

## Implementation Guidelines

- **Language:** Use Python for all Lambda functions.
- **Error Handling:**  
  Ensure you handle API failures gracefully (e.g., non-200 responses, missing data, non-numeric values).
- **Documentation:**  
  Provide inline comments and a README explaining your design decisions.
- **Libraries:**  
  You may use any Python libraries (e.g., `requests`) that help simplify HTTP requests.
- **Step Functions:**  
  Provide a state machine definition (JSON or YAML) that orchestrates your Lambda functions.

---

## Deliverables

1. **Code Repository:**  
   A GitHub (or similar) repository containing your source code, including:
   - Python code for each Lambda function.
   - The AWS Step Functions state machine definition.
   - A README with instructions on how to deploy and test your solution.

2. **Deployed Application:**  
   Either a link to your deployed solution (via API Gateway) or clear instructions for running a local simulation.

---

## Getting Started

1. Review the [SWAPI Documentation](https://swapi.dev/documentation#intro).
2. Design your AWS architecture (Lambda, Step Functions, API Gateway).
3. Implement your solution according to the instructions above.
4. Test your solution thoroughly.
5. Prepare to present your solution and walk through your code.

---

Good luck, and may the Force be with you!

