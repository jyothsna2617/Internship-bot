# Internship-bot
import pyttsx3
import speech_recognition as sr
engine = pyttsx3.init()
def recognize_speech():
    recognizer = sr.Recognizer()
    mic = sr.Microphone()
    with mic as source:
        print("Please say something...")
        recognizer.adjust_for_ambient_noise(source)
        try:
            audio = recognizer.listen(source, timeout=5)  # Adjust timeout as needed (e.g., 5 seconds)
        except sr.WaitTimeoutError:
            print("Timeout. No speech detected.")
            return ""

    try:
        print("Recognizing speech...")
        text = recognizer.recognize_google(audio)
        print(f"You said: {text}")
        return text
    except sr.UnknownValueError:
        print("Sorry, I did not understand that.")
        return ""
    except sr.RequestError:
        print("Sorry, the speech recognition service is unavailable.")
        return ""
# Function to get the bot response
def get_bot_response(input):
    responses = {
        "hello": "Hi there! How can I help you today?",
        "hai": "Hello! How can I assist you?",
        "can you tell me the booking details": "Sure, I can help you with booking an appointment. Please provide your name and preferred date.",
        "what are the services provided": "We offer about internships,application processes, organization info, and more.?",
        "ok thanks": "You're welcome! Have a great day!",
        "cost of apllication": "Rupees 1000. For further details, contact us.",
        "tell me the consultation fee": "Consultation fee is Rupees 500. For further details, contact us.",
        "internship": "We offer internships in tech, marketing, and design. Check our careers page for openings.",
        "application": "Apply online by submitting your resume and cover letter. Shortlisted candidates will be contacted for interviews.",
        "apply": "Apply online by submitting your resume and cover letter. Shortlisted candidates will be contacted for interviews.",
        "organization": "We are a global organization focused on AI and digital transformation.",
        "company": "We are a global organization focused on AI and digital transformation.",
        "contact": "You can reach us at microit@example.com or call plus one two three four five six seven eight nine zero one.",
        "support": "You can reach us at microit@example.com or call plus one two three four five six seven eight nine zero one.",
        "default": "I'm sorry, I didn't understand that. Could you please rephrase?"
    }

    normalized_input = input.lower()
    return responses.get(normalized_input, responses["default"])

def main():
    print("Hi bot can handle about internships, applications, and organizational info..")
    engine.say("Hi bot can handle about internships, applications, and organizational info..")
    print("Hey, I am your Internship bot. How can I assist you today?")
    engine.say("Hey, I am your Internship bot. How can I assist you today?")
    engine.runAndWait()

    while True:
        user_input = recognize_speech()  # Use speech recognition for input

        if not user_input:
            continue  # Continue if no input is recognized

        if "thank you" in user_input.lower():
            engine.say("It's my pleasure")
            engine.runAndWait()
            print("Bot: It's my pleasure")
            break  # Exit after thank you

        bot_response = get_bot_response(user_input)
        print(f"Bot: {bot_response}")
        engine.say(bot_response)
        engine.runAndWait()

if __name__ == "__main__":
    main()
