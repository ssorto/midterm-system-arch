# Full Pseudocode: Context and Survey Design Approach
This pseudocode outlines the structure of the AI-driven interactive survey system, 
including survey setup, user interaction, and response processing.

## Survey Setup (Pre-set Topic)
Function setupSurvey():
    Set surveyTopic = "Reflection"
    
    Display "¡Bienvenidos! Welcome to your personal reflection game."
    Display "Think of this as your own deck of Lotería cards—each one revealing a different part of your day."
    Display "Which card will you draw first? Each one carries meaning, like the cards in a Lotería game."

    Display "A - El Sol ☀️ (Excitement) - A card of energy and light. What moments lit up your day?"
    Display "B - La Luna 🌙 (Uncertainty) - A card of mystery and the unknown. What left you wondering today?"
    Display "C - El Diablo 🔥 (Frustration) - A card of challenge and mischief. What tested your patience today?"
    
    Proceed to tile selection


## User Interaction Layer (Computer 1 - Subscriber)
Function handleUserInput(input):
    If input in ["A", "B", "C"]:  # Supports multiple selections
        Store selectedTiles = input
        Send tile selection to Communication Layer (MQTT)
        Display "You chose: " + selectedTiles
        Display "Let's start with one and see where your reflection takes you."
    Else:
        Display "Oops! Please choose at least one tile."

## Communication Layer (MQTT)
Function transmitUserData(input):
    Convert input into JSON format
    Publish JSON message to MQTT topic "survey/input"

Function receiveAIResponse():
    Subscribe to MQTT topic "survey/response"
    If AI-generated question received:
        Send to Output & Feedback System for display


## AI Processing Layer (Computer 2 - Publisher)
Function processAIResponse(userInput, previousResponses):
    If userInput is valid:
        Retrieve survey knowledge (Reflection context)
        
        Call Gemini AI:
            - Provide context: "User is in a guided reflection experience inspired by Lotería."
            - Provide user response as input
            - Provide previous user responses (if available)
            - Request: "Generate a natural, thoughtful follow-up question to deepen the user's reflection.
                        Reference the meaning of their chosen card (Excitement, Uncertainty, Frustration) 
                        in a way that encourages storytelling.
                        Ensure the question is open-ended, avoiding yes/no or single-word responses.
                        Keep it conversational, engaging, and inviting, as if guiding them through a journey."
        
        AI generates follow-up question
        Send AI-generated question to Communication Layer (MQTT)
    Else:
        Display "Error: Invalid response"


## Output & Feedback System
Function displayAIQuestion(question, previousResponses):
    Display "Question: " + question

    Call Gemini AI:
        - Provide question context
        - Provide previous user responses
        - Request: "Generate a short, conversational prompt to help the user expand on their response.
                    Encourage specific examples or storytelling.
                    Make it feel natural, guiding them toward deeper reflection without making it feel forced."

    AI generates helper text
    Display "Helper Text: " + AI-generated helper text

### Track User Progress
Function updateProgressTracker(userInput, previousResponses):
    Increment completedTiles
    RemainingTiles = TOTAL_TILES - completedTiles
    
    If RemainingTiles > 0:
        Call Gemini AI:
            - Provide user’s past responses and selected tiles
            - Request: "Generate a progress message that feels like a storytelling journey. 
                        Reference the user’s selected cards and encourage them to continue at their own pace.
                        Make it inviting and reflective, ensuring it feels like their choice."

        AI generates progress message
        Display progress message

        Display "Would you like to continue or wrap up here?"
    Else:
        Display "You’ve gathered deep insights. Let’s wrap up with a summary."

### Generate & Display Session Summary
Function generateSessionSummary():
    If user completes all tiles OR chooses to finish:
        
        Call Gemini AI:
            - Provide all user responses
            - Request: "Summarize the user's key reflections in a storytelling format, referencing the cards they chose. 
                        Highlight patterns across responses and connect them meaningfully.
                        Avoid simply listing responses—offer insights that synthesize their reflection.
                        Close with an encouraging reflection that feels like the end of a journey."
        
        AI summarizes key themes from user responses
        AI highlights positive patterns or insights

        Display "Here’s what you reflected on today:"
        Display summary to user
        
        Call Gemini AI:
            - Provide summary
            - Request: "Generate a short, encouraging final message to close the session."

        AI generates closing message
        Display "Helper Text: " + AI-generated closing message

        Ask user: "Would you like to save or share your insights?"
        Save session data


# Annotated Version of Pseudocode for Diagram
This annotated pseudocode describes the survey system flow, mapping directly to  
the architecture diagram. Each function represents a key system component.

## Survey Setup (User Entry Point)
Function setupSurvey():
    Display welcome message
    Prompt user with a soft-start reflection question
    Present emotion tile options (Excitement, Uncertainty, Frustration)
    Allow user to select a tile by pressing a key "A","B", "C"

## User Input Handling
Function handleUserInput(input):
    Validate input (ensure it matches available tiles)
    Store selected tiles
    Send input to Communication Layer (MQTT)
    Display confirmation message to user

## Communication Layer (Data Exchange - MQTT)
Function transmitUserData(input):
    Convert input to JSON format
    Publish JSON message to MQTT topic "survey/input"

Function receiveAIResponse():
    Subscribe to MQTT topic "survey/response"
    Forward received AI-generated question to Output System

## AI Processing (Computer 2 - Publisher)
Function processAIResponse(userInput, previousResponses):
    Retrieve context (Survey reflection model)
    Call AI to generate an open-ended follow-up question
    Convert AI-generated question to JSON format
    Send JSON response back to Communication Layer

Function convertAIOutputToJSON(ai_response):
    Create JSON structure:
        "question" = ai_response
        "timestamp" = getCurrentTimestamp()
        "response_type" = "text"
    Return JSON

## Output & Feedback System (Displaying AI Prompts & Progress)
Function displayAIQuestion(question):
    Show AI-generated reflection question
    Show helper text to guide user response

Function updateProgressTracker():
    Track completed tiles
    Prompt user to continue or exit reflection session

### Session Summary & Completion
Function generateSessionSummary():
    Summarize key insights based on user responses
    Display final reflection message
    Offer option to save or share session summary

