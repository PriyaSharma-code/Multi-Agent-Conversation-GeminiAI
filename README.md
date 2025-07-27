# Multi-Agent-Conversation-GeminiAI

# 📘 Lesson 1: Multi-Agent Conversation and Stand-up Comedy with Gemini API

"""
Required Packages:
- google-generativeai: https://pypi.org/project/google-generativeai/
Install via pip:
    pip install google-generativeai
"""

# STEP 1: Imports and Setup
import os
import google.generativeai as genai
import random
import time

# STEP 2: Load Gemini API Key
# It's best to set this via environment variable for security
GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")

if not GEMINI_API_KEY:
    raise ValueError("❌ GEMINI_API_KEY is not set. Please export it as an environment variable.")

genai.configure(api_key=GEMINI_API_KEY)

# STEP 3: Create a Gemini Model
model = genai.GenerativeModel("gemini-pro")

# STEP 4: Define Agent Characters
agents = [
    {"name": "Alice", "role": "Curious Student"},
    {"name": "Bob", "role": "Philosopher"},
    {"name": "Charlie", "role": "Stand-up Comedian"},
]

# STEP 5: Conversation Context
conversation_context = """
This is a multi-agent interaction. Alice is a curious student asking questions.
Bob is a philosopher giving deep answers. Charlie interrupts with jokes and witty comments.

Let’s explore the topic: 'What is the meaning of life?'
Make it engaging, funny, and informative.
"""

# STEP 6: Start Conversation
prompt = conversation_context + "\nStart the conversation between Alice, Bob, and Charlie."

response = model.generate_content(prompt)

# STEP 7: Print the First Response
print("🧠 Gemini Response:\n")
print(response.text)

# STEP 8: Continue the Conversation Dynamically
for i in range(3):  # Simulate 3 rounds
    print(f"\n--- Round {i + 2} ---")
    
    agent = random.choice(agents)
    next_prompt = f"\n[{agent['name']} the {agent['role']}] continues the conversation:\n"

    try:
        response = model.generate_content(conversation_context + next_prompt)
        print(f"{agent['name']}:")
        print(response.text)
    except Exception as e:
        print(f"⚠️ Error generating content: {e}")
    
    time.sleep(1.5)
