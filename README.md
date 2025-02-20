# AI-Driven Adaptive Survey System
## Assignment - System Architecture & Pseudocode for Midterm
This assignment explores an AI-driven, Lotería-inspired survey system designed to enhance user engagement in qualitative surveys. Unlike static survey designs, this system allows participants to select emotion-based tiles, triggering AI-generated follow-up questions tailored to their responses.

What is Lotería?
Lotería is a traditional Mexican game similar to Bingo, where players match illustrated cards with symbolic meanings to a board. Each card represents a unique concept, emotion, or figure from everyday life and folklore. This survey experience draws inspiration from Lotería by allowing users to select 'tiles' representing emotions to guide their reflection journey.

The goal is to create an interactive and adaptable feedback mechanism that encourages deeper reflections and higher-quality responses from users.

===

## How the System Works
The system is structured in five main layers, each playing a role in facilitating the survey experience:

### Survey Setup (Pre-set Topic)

1. The system initializes with a pre-defined survey topic ("Reflection")
Users are introduced to the process and guided on how to select a tile.
User Interaction Layer (Tile Selection)

2. Users select a tile (mapped to emotions like Excitement, Uncertainty, Frustration).
This selection triggers an event that is sent to the AI processing system.
Communication Layer (MQTT)

3. The selected tile and user input are converted into JSON format and sent via MQTT messaging.
This acts as the bridge between the User Interaction Layer and AI Processing Layer.
AI Processing & Response Generation

4. The system receives the user's selection and determines an AI-generated follow-up question.
This question is tailored based on the emotion associated with the chosen tile.
Output & Feedback System

5. The generated question is displayed with helper text to encourage a more meaningful response.
Users track their progress ("X out of Y responses completed").
After answering, they can either continue or end the session, at which point a summary is displayed.

## Understanding the System Architecture Diagram
The diagram illustrates the movement of data through the system:

* Survey Setup → User is welcomed and provided instructions.
* User Interaction Layer → User selects an emotion tile (A, B, or C).
* Communication Layer (MQTT) → Converts the user’s selection into JSON and passes it to the AI.
* AI Processing Layer → Receives tile selection, processes it, and generates a relevant question.
* Output & Feedback System → Displays the AI-generated question and tracks session progress.

How Information Moves Through the System

* User selects a tile → The selection is captured in the User Interaction Layer.
* MQTT sends data → The tile selection is formatted into JSON and sent to the AI Processing Layer.
* AI generates a follow-up question → Based on the emotion associated with the tile.
* The generated question is displayed → Along with helper text to guide the user’s response.
* User answers & progress is tracked → User can either continue or finish the session.
* Session Summary → If the user finishes, a summary is displayed before the session ends.

## Pseudocode Reference
Diagram has high-level pseudocode, for a more detailed breakdown refer to the pseudocode file (pseudocode.md), which includes:

* Context for game inspiration.
* Survey design logic.

===

## Next Steps for Future Development
Refine AI prompting for optimal user engagement using UXR and survey design best practices.
The AI-generated questions should be iteratively tested to ensure they elicit rich, insightful responses from users. This involves:

* Evaluating whether helper text successfully guides user responses.
* Experimenting with question phrasing to balance open-ended vs. structured responses.
* Testing different prompting styles (e.g., reflective vs. action-oriented) to see what resonates most with participants.

Expand to six tiles for a more diverse emotional spectrum.
Currently, the system supports three emotion categories (Excitement, Uncertainty, Frustration). Expanding to six distinct emotions will:

* Capture a broader range of user experiences.
* Reduce response bias by providing more nuanced choices.
* Improve survey flexibility, allowing for more targeted insights across different research topics.

Explore how the system can be adapted for different survey topics.
The current version is preset for a reflection-based survey, but this system could be generalized for various use cases, such as:

* Product feedback surveys → Users select tiles representing their emotions about a product experience.
* Employee experience tracking → Employees select tiles reflecting their daily work experience.
* Patient feedback in healthcare → Adapt the tool for wellness check-ins or medical experiences.
* Education & learning assessments → Use tiles to help students reflect on their learning experiences.
