# -*- coding: utf-8 -*-
"""
Created on Sat Apr 21 13:21:29 2018

@author: Vrunda B Shah
"""

# -*- coding: utf-8 -*-
"""
Created on Mon Mar 12 02:09:37 2018

@author: Vrunda B Shah
"""

# -*- coding: utf-8 -*-
"""
Created on Sun Mar 11 23:20:51 2018

@author: Vrunda B Shah
"""

from tweepy.streaming import StreamListener
from tweepy import OAuthHandler
from tweepy import Stream
import time


#consumer key, consumer secret, access token, access secret.
consumer_key="Ss9UEEh67HNnONa4xGsgEROhd"
consumer_secret="0QEaNANkFdfDhQ2po405k31QSiOMohkzcvo3bYSnk7i9MDwYEV"
access_token= "973059495155793922-rlXumLFiYg5L0KcnxjQlsOfqpo9cJDw"
access_token_secret="EfSFxMkn8OYVv0j6Wh18m1tTTOxyudwtFebtzIxxyqKdD"

class listener(StreamListener):

    def on_data(self, data):
        try:
            
            print(data)
          #  tweet = data.split(',"text":"')[1].split('","source')[0]
            tweet = data
            #print(data)
            saveThis = tweet
            saveFile = open('stanford.csv','a')
            saveFile.write(saveThis)
            saveFile.write('\n')
            saveFile.close()
            return True
        except BaseException, e:
            print 'failed on data,',str(e)
            time.sleep(5)

    def on_error(self, status):
        print "Fail"
try:
    auth = OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_token, access_token_secret)
    twitterStream = Stream(auth, listener())
    twitterStream.filter(track=['lungcancer','lung cancer','lungcancerawareness'])
    #twitterStream.filter(track=['AmericanCancer','lungcancerawareness','lung cancer','lungcancer','lcsm','lung','lungcancerwalk'])
except BaseException, e:
     print 'failed on data1,',str(e)
    
