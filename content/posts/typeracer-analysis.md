---
title: "How I improved my typing speed and how you can too!"
date: 2019-11-25T23:18:05+05:30
draft: false
featured_image: "https://miro.medium.com/max/8690/0*xc-UnTMdAKK0ZfZ3"

tags: ['natural language processing']
categories: ['NLP']
---

*I was able to get hold of the data used in the following analysis, courtesy of Noah, creator and maintainer of [TypeRacer Data, a third party information center for TypeRacer.](http://www.typeracerdata.com/about)*

Ever wondered what influences your typing speed? Well there are various
resources which can help you polish your technique but there’s more to it than
just touch typing and finger placement. 

Most of the time I am asked this question — **how did I improve my typing speed to achieve a speed of over 100 words per minute?**

### Consistency is Key

In October 2015, in my endeavour to improve my typing speed I stumbled upon
[Typeracer](https://play.typeracer.com/), a website dedicated to type racing
against random people on the internet. Little did I know that the site was
generating a gold mine of data and I would be a contributor of the same. Since
then I have completed more than 4000 races in the past 3 years and my
improvement over time is evident from the following graph —

{{< figure src="https://cdn-images-1.medium.com/max/1000/1*YdJ0wkPxvAUrmzVn4WtioQ.png" title="Scatter plot of all my races" >}}

I started with a mere 58 Words Per Minute (WPM) in 2015 and now average over 95
WPM with a highest score of 128 WPM.

{{< figure src="https://cdn-images-1.medium.com/max/750/1*TgyRGSSQm7MUVGegjFNBEA.png" title="Number of races played across the years" >}}

I completed over 3000 races in 2016 and 2017 combined. This number might be
dwarfed by other people on the website easily, but for me it was the sheer
quantity and consistency that allowed me to raise my bar higher.

<br> 

### Progress over time

{{< figure src="https://cdn-images-1.medium.com/max/1500/1*45rl-A0smsxHhSiw_vykvw.png" title="Box plot of all my races over time" >}}

According to my race data, I used to play 125 races in a month on an average
which helped me register the most frequent words in my muscle memory. 

You can see that there’s a dip in the months of May, June and July during which
I had my year end exams. After that there was a consistent increase in my
average WPM in the following months. These breaks kind of helped me rejuvenate
my typing game.

2018 is an exception since the sample space over which the graph has been plotted is way less than the other years. As you can see in the “Count vs Year” graph above, I played only 250 games in the year of 2018.

### About the data

{{< figure src="https://cdn-images-1.medium.com/max/750/1*nZeo7p0OtZYLV-t7c7vDag.png" title="Texts added gradually over time" >}}

There are over 5200 active texts site wide used in the races. Most of these
texts are
[user-contributed](https://docs.google.com/spreadsheets/d/1CReWQkUlUHdDiOo6nz_0O5KBmeXIzqVyY_83p-njoog/edit#gid=1397097667)
and eventually moderated. 

2017 saw an influx in inclusion of new texts mainly because there was a push to
increase the number of texts when a user complained about repetition and lack of
variety according to [this blog in Jan
2017.](https://blog.typeracer.com/2017/01/16/typeracer-passes-2000-quotes/)

As of Dec 2018, the longest text in terms of number of characters is **861
character long **while the shortest text is **44 character long** and is a
sentence which encompasses all the alphabets in English — 

    The quick brown fox jumps over the lazy dog.

There is a **difficulty rating** associated with each text and according to the
[FAQ](http://www.typeracerdata.com/about) it is calculated by first evaluating
personal difficulty rating of each text for a user and then averaging it over
all the users to obtain an overall difficulty rating for a particular text.

It ranges from 0.599 to 1.433 for the given texts — higher the value, lesser the
difficulty. One of the most difficult texts on site according to the difficulty
rating is — 

    "This man right here," McGuinness said, pointing at Kenna, 
    "he\'s going to change the world." That was his instinctive 
    feeling, and the manager of a band like U2 is a man who knows music.

while the easiest text to type is — 

    They don't know that we know they know we know.

The **top score** on the website is **3600** **WPM** (Words per minute) (which
seems impossible even with a modern stenographer keyboard) while the text which
has the **least top score** of **151 WPM** achieved on is — 

    Waiter: What is your name? Aladeen: Allison Burgers. Waiter: 
    That's a made up name. What's your real name? Aladeen: My name 
    is Ladiz. Waiter: Ladiz what Aladeen: Ladiz Washroom. Waiter: 
    So your name is like the sign. Ladies washroom? That is a made 
    up name, what is your real name? I am interested. We are interested. 
    Aladeen: Emplyes. Waiter: Emplyes what!? Aladeen: Emplyes Mustwashhands. 
    Waiter: That is a made up name. What is your real name. Aladeen: 
    Max. Waiter: Max what? Aladeen: Imumoccupancy120. Waiter: There's 
    a number in the name? WHO ARE YOU!?

This led me to the question —

#### What influences our speed while typing?

While external factors (keyboard, finger position, touch typing, wrist posture
etc.) do contribute in helping improve our speeds, we’ll focus on the text this
time. 

The above pieces of texts are indicative of speed/difficulty change due to
increased number of **punctuation, capital letters and length of text.** 

The following graph shows a change in difficulty rating across the above
mentioned three factors on a subset of texts which I have typed.

{{< figure src="https://cdn-images-1.medium.com/max/1000/1*YVJXxXC6DC3Au0Ssmt7u9A.png" title="Speed(WPM) across length of text, number of punctuations and capital letters in it." >}}

The above graph makes it clear that — 

1.  As the length of the text increases, there’s bound to be a drop in your normal
speeds. Factors such as stamina and concentration affect our ability to maintain
our speed throughout. It’s like running a marathon vs a sprint.
1.  Punctuation in texts become obstacles because you have to travel more distance
on the keyboard to reach those keys. And sometimes an extra “Shift” key needs to
be used. Unless you have memorized all the punctuations on the keyboard it is
bound to reduce your speed.
1.  Similarly, capital case letters require the use of “Shift” or “Caps” which
causes a person to slow down relatively. 

#### Can we predict the typing speed based only on the text?

Now that we’ve established some features which directly affect typing speed, we
can use those in conjunction with the sentence itself to predict the typing
speed.

I proposed this prediction task as a classification problem by bifurcating the
races into a three classes — 

1.  Between 75 and 85 WPM (1171 samples)
1.  Between 85 and 95 WPM (960 samples)
1.  Above 95 (446 samples)

For the most part, I decided on these classes arbitrarily with an optimistic
assumption that even my worst races wouldn’t go below 75 WPM. 

To convert sentences into their vector representation I used a simple [sklearn
TfidfVectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html).
Since all the words in a sentence are useful for our analysis, I didn’t exclude
stop words as well as turned off the lowercase feature in the Vectorizer.
Eventually I concatenated all the following features and mapped them to the
three classes  — 

1.  A sparse matrix of features calculated via TfidfVectorizer
1.  Length of text
1.  Number of punctuations 
1.  Number of capital letters
1.  Accuracy
1.  Difficulty rating

Using Logistic Regression I managed to achieve an accuracy of 49.8% which is pretty bad and only better than random chance of 33.33%.

The whole point of doing this exercise is to explore what kind of features would be useful to evaluate a person’s typing speed. With the kind of accuracy achieved using the current features and model, it seems we would require more feature engineering and a better model to get a descent accuracy score.

### Conclusion

1. We learnt how consistent practising can help improve your typing speed.
2. We also saw the effects of punctuation, capital case and length of text on the overall typing speed.
3. And we explored whether these features would be useful in a simple classification task.

### Future Scope

Better features can be extracted by running the sentences through an LSTM to obtain intermediary features. This will allow us to include word order in the text as a feature. This will help the model to learn frequent patterns of words which appear in conjunction.

Another way to reinforce the model is to feed the words which are frequently mis-typed. A more complex but useful data would be the flight time between two letters. This data, then, can also be used to build keystroke behavioural profiles of each person.

---

All the data and code for this blog can be found [here](https://github.com/nirajpandkar/typeracer-analysis).
