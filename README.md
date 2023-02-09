# Sample
Demo
import pyttsx3 
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import smtplib
import time
import ctypes
import subprocess
import pywhatkit as pwt

engine=pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
print(voices[1].id)
engine.setProperty('voice',voices[1].id) 
def speak(audio):
    engine.say(audio)
    engine.runAndWait()
   
def WishMe():
    hour= int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning!")
    elif hour>=12 and hour<18:
        speak("Good Afternoon!")
    else:
        speak("Good Evening!")
    speak ("I am EDITH BOSS,How may I help you?")
def takeCommand():
    #it takes microphone input from the user and  returns string  output 
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening..")
        r.pause_threshold = 1
        audio =r.listen(source)
    try:
        print("Recognizing....")
        query =r.recognize_google(audio,language='en-in')
        print(f"User said:{query}\n")
    except Exception as e:
        #print(e)
        print("Say it again Kindely..")
        return"None"
    return query
def record_audio():
    with sr.Microphone() as source:
        audio=sr.listen(source)
        voice_data=""
        try:
            voice_data=sr.Recognizer_google(audio)
            print(voice_data)
        except sr.UnknownValueError:
            print('sorry, Kindly tell me again sir')
        except sr.RequestError:
            print("sorry,My speech analysis is going on....")
        return voice_data
   
def sendEmail(to,content):
    server =smtplib.SMTP('smpt.gmail.com',465)
    server.ehlo()
    server.starttis()
    server.login('gk5139272@gmail.com','Krishnan@3010')
    server.sendmail('gk5139272@gmail.com,to,content')
    
if __name__=="__main__":
    WishMe()
    while True:
    #if 1:   
        query=takeCommand().lower()   
        if'wikipedia' in query:
            speak('searching wikipedia...')
            query=query.replace("Wikipedia","")
            results=wikipedia.summary(query,sentences=2)
            speak("Acoornding to wikipedia")
            print(results)
            speak(results)
            
        elif 'open youtube' in query:
            webbrowser.open("YOUTUBE.com")
        elif 'open google' in query:
            webbrowser.open("google.com")
        elif 'open stackoverflow' in query:
            webbrowser.open("stackoverflows.com")
        elif 'open instagram' in query:
            webbrowser.open("https://www.instagram.com/")
        elif 'play music' in query:
            music_dir='C:\\Users\gk513\\OneDrive\Desktop\\Uncle sathish\\Song'
            songs =os.listdir(music_dir)
            print(songs)
            os.startfile(os.path.join(music_dir,songs[0]))
        
        elif 'the time' in query:
            strTime =datetime.datetime.now().strfttime("%H:$M:%S")
            speak(f"Sir,The time is {strTime}")
        elif 'open code' in query:
            codepath="C:\\Users\\gk513\\AppData\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codepath)
        elif'email to gopal' in query:
            try:
                speak("What should I Say")
                content =takeCommand()
                to ="gk5139272@gmail.com"
                sendEmail(to,content)
                speak("Email has been sent!")
            except Exception as e:
                print(e) 
                speak("Sorry Krish jr , I am not able send this email at momentum ")
        elif "who created you" in query:
            speak("I have been created by Krish jr.")
        elif "who made you to come this world" in query:
            speak("Thanks to Krish jr. further It's a secret")
        elif "who are you" in query:
            speak("I am your A.I created by Krish jr")
        elif "who is krish junior" in query:
            speak("He is my owner,he bring me to this world")
        elif "lock window" in query:
            speak("locking the device")
            ctypes.windll.user32.LockWorkStation()
        elif "shutdown system" in query:
            speak("Hold On a Sec ! Your system is on its way to shut down")
            subprocess.call('shutdown / p /f')
        elif "don't listen" in query or "stop listening" in query:
            speak("for how much time you want to stop EDITH  from listening commands")
            a = int(takeCommand())
            time.sleep(a)
            print(a)
        elif "restart" in query:
            subprocess.call(["restart", "/r"])
        elif "hibernate" in query or "sleep" in query:
            speak("Hibernating")
            subprocess.call("shutdown / h")
        elif "how are you" in query:
            speak("I'm fine, glad you me that")
        elif "i love you" in query:
            speak("It's hard to understand")
        elif "bye" in query:
            speak("Thank sir , let meet again")
            subprocess.call('shutdown / p /f')
        elif 'search' in query:
            speak("What should I want to search")
            tool=takeCommand()
            results=pwt.search(tool)
