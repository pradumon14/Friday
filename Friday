import speech_recognition as sr
import pyttsx3
import openai

openai.api_key = "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"
def speak(text):
    engine = pyttsx3.init()
    voices = engine.getProperty("voices")
    engine.setProperty("voice", voices[0].id)
    engine.setProperty("rate", 150)
    engine.say(text)
    engine.runAndWait()
    engine.stop()

def recognize_speech():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        audio = r.listen(source)
        try:
            return r.recognize_google(audio)
        except Exception as e:
            return None

def respond(prompt):
    model_engine = "text-davinci-003"
    completion = openai.Completion.create(
        engine=model_engine,
        prompt=prompt,
        max_tokens=1024,
        n=1,
        stop=None,
        temperature=0.5,
    )
    response = completion.choices[0].text
    return response

def start_conversation():
    while True:
        prompt = recognize_speech()
        if prompt is None:
            speak("Sorry, I didn't catch that. Could you repeat it?")
        elif prompt.lower() == "exit":
            break
        else:
            response = respond(prompt)
            speak(response)

start_conversation()
