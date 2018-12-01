""" ENTER YOUR OWN CREDENTIALS refers to the credentials you will receive when you obtain your twitter developers account.
They are relevant to you, so will be different for different users, so put in your own"""

#Import the necessary methods from tweepy library
from tweepy.streaming import StreamListener
from tweepy import OAuthHandler
from tweepy import Stream
import sys
import json


#MODE = CONSOLE means content of tweets will be displayed to console
#MODE = FILESAVE means content of tweets will be saved to the file tweets.txt
MODE = "FILESAVE"

#Refined refers to whether we filter the tweets (based on characters such as @ or http
#or ':') at the end of 
REFINED = True


#How we refine/cleanup the data
def clean_up(string):
    new_string = " ".join(list(filter(lambda x:((x[0] != '#') and (x[0] != '@') and ((len(x) >= 1) and x[-1] != ':') and ((len(x) <= 3) or (x[0:4] != 'http')) and ((len(x) <= 1) or x[0:2] != 'RT')), string.split())))
    if (len(new_string) != 0) and new_string[-1] != '.':
        new_string = new_string + '.'
    return new_string



#Variables that contains the user credentials to access Twitter API 
consumer_key= 'ENTER YOUR OWN CREDENTIALS'
consumer_secret= 'ENTER YOUR OWN CREDENTIALS'
access_token= 'ENTER YOUR OWN CREDENTIALS'
access_token_secret= 'ENTER YOUR OWN CREDENTIALS'

args = sys.argv
if len(args)>= 2:
    args = args[1]
else:
    args = 0



#This is a basic listener that just prints received tweets to stdout.
class StdOutListener(StreamListener):

    def on_data(self, data):
        data = json.loads(data)
        if "text" in data:
            if MODE == "CONSOLE":
                if REFINED:
                    print(clean_up(data["text"]))
                else:
                    print(data["text"])
            if MODE == "FILESAVE":
                if REFINED:
                    f.write(clean_up(data["text"]) + u"\n")
                else:
                    f.write(data["text"] + u"\n")
        return True

    def on_error(self, status):
        #print(status)
        return

if __name__ == '__main__':

    if MODE == "FILESAVE":
        f= open("tweets.txt","w+", encoding='utf-8')
    
    #This handles Twitter authetification and the connection to Twitter Streaming API
    def exec():
        
        try:
            l = StdOutListener()
            auth = OAuthHandler(consumer_key, consumer_secret)
            auth.set_access_token(access_token, access_token_secret)
            stream = Stream(auth, l)
         
        
            #This line filter Twitter Streams to capture data by the keywords: 'python', 'javascript', 'ruby'
            if args != 0:
                stream.filter(languages=["en"], track=args)
            else:
                stream.filter(languages=["en"], track=["a", "the", "i", "you", "u"])
        #except(HTTPError, URLError) as error:
            #exec()
        except Exception as e:
            exec()
        else:
            exec()
    exec()
    
    if MODE == "FILESAVE":
        f.close()
