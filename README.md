import streamlit as st
import random
from datetime import datetime

st.set_page_config(page_title="Mental Health Chatbot", page_icon="🧠")

st.title("🧠 Mental Health Check-In Chatbot")
st.markdown("This chatbot checks in on your feelings, shares kind thoughts, and helps you track your mood. 💬")

# Initialize session state
if 'mood_log' not in st.session_state:
    st.session_state.mood_log = []

# Emotional keywords and responses
emotions = {
    "sad": "I'm sorry you're feeling sad. Remember, it's okay to take time for yourself.",
    "happy": "That's wonderful to hear! Keep enjoying the good moments.",
    "angry": "Anger is a natural feeling. Try to breathe and take a little break.",
    "tired": "Rest is important. Maybe take a short nap or relax with something you enjoy.",
    "anxious": "Anxiety can be tough. Try to focus on your breathing and ground yourself.",
    "lonely": "You’re not alone. Reaching out to someone you trust can help.",
}

# Positive quotes
quotes = [
    "You are stronger than you think.",
    "This too shall pass.",
    "Your feelings are valid.",
    "You don't have to do everything today.",
    "Small steps are still progress.",
]

# Daily tip
daily_tips = [
    "Take a deep breath and hold for 5 seconds before slowly exhaling.",
    "Write down 3 things you’re grateful for today.",
    "Drink a glass of water. Hydration helps your brain function better.",
    "Go outside for 10 minutes and feel the sun or breeze.",
    "Talk to someone you trust about how you're feeling.",
]

st.markdown(f"🌞 **Daily Tip:** _{random.choice(daily_tips)}_")

user_input = st.text_input("How are you feeling today?")

if user_input:
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M")
    mood_entry = {"time": timestamp, "text": user_input}
    st.session_state.mood_log.append(mood_entry)

    found = False
    for emotion, response in emotions.items():
        if emotion in user_input.lower():
            st.write("🤖: " + response)
            st.success(f"💡 Positive Thought: "{random.choice(quotes)}"")
            found = True
            break

    if not found:
        st.write("🤖: Thanks for sharing. Whatever you're feeling, it's okay. 🌿")
        st.success(f"💡 Positive Thought: "{random.choice(quotes)}"")

    st.subheader("📈 Mood Tracker")
    for entry in reversed(st.session_state.mood_log):
        st.write(f"{entry['time']} - _{entry['text']}_")

    st.subheader("📝 Leave Feedback")
    feedback = st.text_area("Any suggestions or feedback?")
    if feedback:
        st.success("Thank you for your feedback! 💬")

        
