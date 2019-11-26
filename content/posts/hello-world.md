---
title: "Hello World"
date: 2019-11-25T23:18:05+05:30
draft: true

tags: ['deeplearning', 'natural language processing']
categories: ['Introduction']
---

How I improved my typing speed and how you can too!
I was able to get hold of the data used in the following analysis, courtesy of Noah, creator and maintainer of TypeRacer Data, a third party information center for TypeRacer.
Ever wondered what influences your typing speed? Well there are various resources which can help you polish your technique but there's more to it than just touch typing and finger placement. 
Consistency is Key
In October 2015, in my endeavour to improve my typing speed I stumbled upon Typeracer, a website dedicated to type racing against random people on the internet. Little did I know that the site was generating a gold mine of data and I would be a contributor of the same. Since then I have completed more than 4000 races in the past 3 years and my improvement over time is evident from the following graph - 
Scatter plot of all my racesI started with a mere 58 Words Per Minute (WPM) in 2015 and now average over 95 WPM with a highest score of 128 WPM. 
Number of races played across the yearsI completed over 3000 races in 2016 and 2017 combined. This number might be dwarfed by other people on the website easily, but for me it was the sheer quantity and consistency that allowed me to raise my bar higher. 


Progress over time
According to my race data, I used to play 125 races in a month on an average which helped me register the most frequent words in my muscle memory. 
You can see that there's a dip in the months of May, June and July during which I had my year end exams. After that there was a consistent increase in my average WPM in the following months. These breaks kind of helped me rejuvenate my typing game except for 2018 during which I played very few games. 
About the data
Texts added gradually over timeThere are over 5200 active texts site wide used in the races. Most of these texts are user-contributed and eventually moderated. 
2017 saw an influx in inclusion of new texts mainly because there was a push to increase the number of texts when a user complained about repetition and lack of variety according to this blog in Jan 2017.
As of Dec 2018, the longest text in terms of number of characters is 861 character long while the shortest text is 44 character long and is a sentence which encompasses all the alphabets in English - 
The quick brown fox jumps over the lazy dog.
There is a difficulty rating associated with each text and according to the FAQ it is calculated by first evaluating personal difficulty rating of each text for a user and then averaging it over all the users to obtain an overall difficulty rating for a particular text.
It ranges from 0.599 to 1.433 for the given texts - higher the value, lesser the difficulty. One of the most difficult texts on site according to the difficulty rating is - 
"This man right here," McGuinness said, pointing at Kenna, "he\'s going to change the world." That was his instinctive feeling, and the manager of a band like U2 is a man who knows music.
while the easiest text to type is - 
They don't know that we know they know we know.
The top score on the website is 3600 WPM (Words per minute) (which seems impossible even with a modern stenographer keyboard) while the text which has the least top score of 151 WPM achieved on is - 
Waiter: What is your name? Aladeen: Allison Burgers. Waiter: That's a made up name. What's your real name? Aladeen: My name is Ladiz. Waiter: Ladiz what? Aladeen: Ladiz Washroom. Waiter: So your name is like the sign. Ladies washroom? That is a made up name, what is your real name? I am interested. We are interested. Aladeen: Emplyes. Waiter: Emplyes what!? Aladeen: Emplyes Mustwashhands. Waiter: That is a made up name. What is your real name. Aladeen: Max. Waiter: Max what? Aladeen: Imumoccupancy120. Waiter: There's a number in the name? WHO ARE YOU!?
This led me to the question - 
What influences our speed while typing?
While external factors (keyboard, finger position, touch typing, wrist posture etc.) do contribute in helping improve our speeds, we'll focus on the text this time. 
The above pieces of texts are indicative of speed/difficulty change due to increased number of punctuation, capital letters and length of text. 
The following graph shows a change in difficulty rating across the above mentioned three factors on a subset of texts which I have typed.
Difficulty Rating across length of text, number of punctuations and capital letters in it. (Note: Lower the magnitude of the difficulty rating, the more difficult it is to type the text)The above graph makes it clear that - 
As the length of the text increases, there's bound to be a drop in your normal speeds. Factors such as stamina and concentration affect our ability to maintain our speed throughout. It's like running a marathon vs a sprint.
Punctuation in texts become obstacles because you have to travel more distance on the keyboard to reach those keys. And sometimes an extra "Shift" key needs to be used. Unless you have memorized all the punctuations on the keyboard it is bound to reduce your speed.
Similarly, capital case letters require the use of "Shift" or "Caps" which causes a person to slow down relatively. 

Can we predict the typing speed based only on the text?
Now that we've established some features which directly affect typing speed, we can use those in conjunction with the sentence itself to predict the typing speed.
I proposed this prediction task as a classification problem by bifurcating the races into a three classes - 
Between 75 and 85 WPM (1171 samples)
Between 85 and 95 WPM (960 samples)
Above 95 (446 samples)

For the most part, I decided on these classes arbitrarily with an optimistic assumption that even my worst races wouldn't go below 75 WPM. 
To convert sentences into their vector representation I used a simple sklearn TfidfVectorizer. Since all the words in a sentence are useful for our analysis, I didn't exclude stop words as well as turned off the lowercase feature in the Vectorizer. Eventually I concatenated all the following features and mapped them to the three classes  - 
A sparse matrix of features calculated via TfidfVectorizer
Length of text
Number of punctuations 
Number of capital letters
Accuracy
Difficulty rating

I managed to achieve an accuracy of 49% which is pretty bad and only better than random chance of 33.33%. 
Future Scope
Better features can be extracted by running the sentences through an LSTM to obtain intermediary features. This will allow us to include word order of the text which contributes