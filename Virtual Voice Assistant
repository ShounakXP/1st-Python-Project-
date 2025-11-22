import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import requests

# Initialize text-to-speech engine
engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def listen():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language="en-in")
        print("You said:", query)
    except:
        speak("Sorry, I didn't catch that. Please say again.")
        return ""
    return query.lower()

def greet():
    hour = datetime.datetime.now().hour
    if 0 <= hour < 12:
        speak("Good Morning!")
    elif 12 <= hour < 18:
        speak("Good Afternoon!")
    else:
        speak("Good Evening!")
    speak("I am your virtual assistant. How can I help you?")

def get_weather(city):
    try:
        api_key = "https://wttr.in/{}?format=3".format(city)
        weather = requests.get(api_key).text
        return weather
    except:
        return "Unable to fetch weather."

# MAIN PROGRAM
greet()

while True:
    query = listen()

    if "time" in query:
        timeNow = datetime.datetime.now().strftime("%I:%M %p")
        speak(f"The time is {timeNow}")

    elif "date" in query:
        today = datetime.datetime.now().strftime("%d %B %Y")
        speak(f"Today's date is {today}")

    elif "open google" in query:
        speak("Opening Google")
        webbrowser.open("https://www.google.com")

    elif "open youtube" in query:
        speak("Opening YouTube")
        webbrowser.open("https://www.youtube.com")

    elif "weather" in query:
        speak("Which city?")
        city = listen()
        if city:
            speak("Fetching weather information.")
            weather = get_weather(city)
            speak(weather)

    elif "who are you" in query:
        speak("I am your voice assistant, created using Python.")

    elif "hello" in query:
        speak("Hello! How can I help you?")

    elif "stop" in query or "bye" in query or "exit" in query:
        speak("Goodbye! Have a nice day.")
        break

    elif query != "":
        speak("Sorry, I don't know that command yet.")
