# Using AI to take notes of your Teams meeting
This script allows you create a summary of the meeting you recorded in Teams. 

## Installation
Install ffmpeg and sox:
* [ffmpeg](https://github.com/BtbN/FFmpeg-Builds/releases)    
* [sox](https://sourceforge.net/projects/sox/files/latest/download)

Install the Teams Notetaker package by pip installing it from Github:  
```
pip install git+https://github.com/kromme/Teams-Notetaker
```

## Preparations
1. Get the video: From January, 11th 2021 all Teams recordings will be stored in OneDrive directly, see [here](https://docs.microsoft.com/en-gb/MicrosoftTeams/tmr-meeting-recording-change). Until then download it from [Stream](https://web.microsoftstream.com/) > My Content > video > Download video.
2. Setup a [Google Speech API](https://cloud.google.com/docs/authentication/getting-started) and get the `key.json` and save this file in the working directory.
3. Clone this repository: `git clone https://github.com/kromme/Teams-Notetaker.git`

## Run
```
from teams_notetaker import TeamsNotetaker
tn = TeamsNotetaker(filename = 'Meeting.mp4')
tn.run()
```


### Summarization
There are two ways of summarizing texts with the help of AI: Abstractive and Extractive. Abstractive summarization rewrites the whole document, the algorithm interprets the article and then rewrites it in smaller set of sentences. The summarization as we learned it in highschool and university is comparable to the abstractive summarization. Extractive summarization estimates which sentences are the most important. Which technique is better depends on the task at hand, abstractive summarizations mind be better when rewriting essays or creating an introduction for an article. Extractive might be better for highlighting the most important parts of an article.  

For this purpose I've chosen to use extractive summarization for two reasons:
1. It better fits the purpose of the task at hand, my goal is to find the best sentences of a meeting and order them in a way which makes sense to the people in the meeting.  
2. It is computational more efficient than abstractive summarization. For us, humans, it is more difficult to rewrite a document than picking the most important sentences, this also holds for algorithms.  


Have a look how [this article about chatbot paradoxes](https://tailo.nl/chatbotparadox/) is summarized:
> The promise of less customer contact for employees, or the handling of easier questions, make chatbots immensely popular. Chatbot sometimes provides more contact\n\nThe business case for a chatbot is often made to reduce unnecessary customer contact for employees. To answer the easier questions, the chatbot is given a prominent place on the website. As a result of which you, as a customer, are forwarded to an employee. However, as we just saw, the bot often does not yet recognize the intention or the question is asked in a way that the bot has not yet learned.

Or check out the summarization of the [plot of Orwell's book 1984](https://en.wikipedia.org/wiki/Nineteen_Eighty-Four):
> In the year 1984, civilization has been damaged by war, civil conflict, and revolution. Those who fall out of favour with the Party become "unpersons", disappearing with all evidence of their existence destroyed. In London, Winston Smith is a member of the Outer Party, working at the Ministry of Truth, where he rewrites historical records to conform to the state\'s ever-changing version of history. Winston reflects that Syme will disappear as he is "too intelligent" and therefore dangerous to the Party. During his affair with Julia, Winston remembers the disappearance of his family during the civil war of the 1950s and his tense relationship with his wife Katharine, from whom he is separated (divorce is not permitted by the Party). O\'Brien introduces himself as a member of the Brotherhood and sends Winston a copy of The Theory and Practice of Oligarchical Collectivism by Goldstein. Winston is recalled to the Ministry to help make the major necessary revisions of the records. Both reveal betraying the other and no longer possess feelings for one other.