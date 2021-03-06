# jarvis
#importing modules
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes

listener=sr.Recognizer()
engine=pyttsx3.init()
voices=engine.getProperty('voices')
#set index 0 or 1 for male and female voices
engine.setProperty('voice',voices[0].id)

def talk(text):
    engine.say(text)
    engine.runAndWait()
def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            voice=listener.listen(source)
            command=listener.recognize_google(voice)
            command=command.lower()
            if "jarvis" in command:
                command=command.replace('jarvis','')
                print(command)
    except:
        exit()
        pass
    return command


def run_jarvis():
    command=take_command()
    print(command)
    if "play" in command :
        song=command.replace('play','')
        pywhatkit.playonyt(song)
        talk("playing boss!!" + song)
    elif "time" in command:
        time=datetime.datetime.now().strftime("%I:%M %p")
        print(time)
        talk('boss,current time is' + time )
    elif "what" in command:
        person=command.replace('find',"")
        info=wikipedia.summary(person,1)
        print(info)
        talk(info)
    elif "who are you" in command:
        print("I am jarvis (AI) created by my boss JOAN ")
        talk('I am jarvis created by my boss JOAN')
        print("I am under developement")
        talk("i am under developement")
    elif "tell me a joke" in command:
        jokes=pyjokes.get_joke()
        print(jokes)
        talk(jokes)
#add multiple elif statement for more command
    else:
        print('boss,please say the command again !!')
        talk('boss, please say the command again !!')


while True:
    run_jarvis()
