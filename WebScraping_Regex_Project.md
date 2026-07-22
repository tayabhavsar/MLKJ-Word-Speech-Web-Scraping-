Web Scraping + Regular Expression + Pandas 


```python
#link = 'http://analytictech.com/mb021/mlk.htm'
```

Goal: Find out how many times MLKJ used each word in his speech 


```python
from bs4 import BeautifulSoup
import requests 
```


```python
url = 'http://analytictech.com/mb021/mlk.htm'

page = requests.get(url)

soup = BeautifulSoup(page.text, 'html')
```


```python
print(soup)
```

    <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML//EN">
    <html>
    <head>
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
    <meta content="Microsoft FrontPage 4.0" name="GENERATOR"/>
    <title>Martin Luther King Jr.'s 1962 Speech</title>
    </head>
    <body alink="#FF0000" bgcolor="#FFFFFF" link="#0000FF" text="#000000" vlink="#551A8B">
    <h1><font size="5">Transcript of speech by </font><br/>
    Dr. Martin Luther King Jr. <br/>
    August 28, 1963. Lincoln Memorial in Washington D.C. </h1>
    <hr color="#008080" noshade="" size="5"/>
    <p>I am happy to join with you today in what will go down in
    history as the greatest demonstration for freedom in the history
    of our nation. </p>
    <p>Five score years ago a great American in whose symbolic shadow
    we stand today signed the Emancipation Proclamation. This
    momentous decree came as a great beckoning light of hope to
    millions of Negro slaves who had been seared in the flames of
    withering injustice. It came as a joyous daybreak to end the long
    night of their captivity. </p>
    <p>But one hundred years later the Negro is still not free. One
    hundred years later the life of the Negro is still sadly crippled
    by the manacles of segregation and the chains of discrimination. </p>
    <p>One hundred years later the Negro lives on a lonely island of
    poverty in the midst of a vast ocean of material prosperity. </p>
    <p>One hundred years later the Negro is still languishing in the
    comers of American society and finds himself in exile in his own
    land. </p>
    <p>We all have come to this hallowed spot to remind America of
    the fierce urgency of now. Now is the time to rise from the dark
    and desolate valley of segregation to the sunlit path of racial
    justice. Now is the time to change racial injustice to the solid
    rock of brotherhood. Now is the time to make justice ring out for
    all of God's children. </p>
    <p>There will be neither rest nor tranquility in America until
    the Negro is granted citizenship rights. </p>
    <p>We must forever conduct our struggle on the high plane of
    dignity and discipline. We must not allow our creative protest to
    degenerate into physical violence. Again and again we must rise
    to the majestic heights of meeting physical force with soul
    force. </p>
    <p>And the marvelous new militarism which has engulfed the Negro
    community must not lead us to a distrust of all white people, for
    many of our white brothers have evidenced by their presence here
    today that they have come to realize that their destiny is part
    of our destiny. </p>
    <p>So even though we face the difficulties of today and tomorrow
    I still have a dream. It is a dream deeply rooted in the American
    dream. </p>
    <p>I have a dream that one day this nation will rise up and live
    out the true meaning of its creed: 'We hold these truths to be
    self-evident; that all men are created equal." </p>
    <p>I have a dream that one day on the red hills of Georgia the
    sons of former slaves and the sons of former slave owners will be
    able to sit together at the table of brotherhood. </p>
    <p>I have a dream that one day even the state of Mississippi, a
    state sweltering with the heat of injustice, sweltering with the
    heat of oppression, will be transformed into an oasis of freedom
    and justice. </p>
    <p>I have a dream that little children will one day live in a
    nation where they will not be judged by the color of their skin
    but by the content of their character. </p>
    <p>I have a dream today. </p>
    <p>I have a dream that one day down in Alabama, with its vicious
    racists, with its Governor having his lips dripping with the
    words of interposition and nullification, one day right there in
    Alabama little black boys and black girls will be able to join
    hands with little white boys and white girls as sisters and
    brothers. </p>
    <p>I have a dream today. </p>
    <p>I have a dream that one day every valley shall be exalted,
    every hill and mountain shall be made low, the rough places
    plains, and the crooked places will be made straight, and before
    the Lord will be revealed, and all flesh shall see it together. </p>
    <p>This is our hope. This is the faith that I go back to the
    mount with. With this faith we will be able to hew out of the
    mountain of despair a stone of hope. With this faith we will be
    able to transform the genuine discords of our nation into a
    beautiful symphony of brotherhood. With this faith we will be
    able to work together, pray together; to struggle together, to go
    to jail together, to stand up for freedom forever, )mowing that
    we will be free one day. </p>
    <p>And I say to you today my friends, let freedom ring. From the
    prodigious hilltops of New Hampshire, let freedom ring. From the
    mighty mountains of New York, let freedom ring. From the mighty
    Alleghenies of Pennsylvania! </p>
    <p>Let freedom ring from the snow capped Rockies of Colorado! </p>
    <p>Let freedom ring from the curvaceous slopes of California! </p>
    <p>But not only there; let freedom ring from the Stone Mountain
    of Georgia! </p>
    <p>Let freedom ring from Lookout Mountain in Tennessee! </p>
    <p>Let freedom ring from every hill and molehill in Mississippi.
    From every mountainside, let freedom ring. </p>
    <p>And when this happens, when we allow freedom to ring, when we
    let it ring from every village and hamlet, from every state and
    every city, we will be able to speed up that day when all of
    God's children, black men and white men, Jews and Gentiles,
    Protestants and Catholics, will be able to join hands and sing in
    the words of the old Negro spiritual, "Free at last! Free at
    last! Thank God almighty, we're free at last!" </p>
    </body>
    </html>
    
    


```python
mlkj_speech = soup.find_all('p')
```


```python
mlkj_speech
```




    [<p>I am happy to join with you today in what will go down in
     history as the greatest demonstration for freedom in the history
     of our nation. </p>,
     <p>Five score years ago a great American in whose symbolic shadow
     we stand today signed the Emancipation Proclamation. This
     momentous decree came as a great beckoning light of hope to
     millions of Negro slaves who had been seared in the flames of
     withering injustice. It came as a joyous daybreak to end the long
     night of their captivity. </p>,
     <p>But one hundred years later the Negro is still not free. One
     hundred years later the life of the Negro is still sadly crippled
     by the manacles of segregation and the chains of discrimination. </p>,
     <p>One hundred years later the Negro lives on a lonely island of
     poverty in the midst of a vast ocean of material prosperity. </p>,
     <p>One hundred years later the Negro is still languishing in the
     comers of American society and finds himself in exile in his own
     land. </p>,
     <p>We all have come to this hallowed spot to remind America of
     the fierce urgency of now. Now is the time to rise from the dark
     and desolate valley of segregation to the sunlit path of racial
     justice. Now is the time to change racial injustice to the solid
     rock of brotherhood. Now is the time to make justice ring out for
     all of God's children. </p>,
     <p>There will be neither rest nor tranquility in America until
     the Negro is granted citizenship rights. </p>,
     <p>We must forever conduct our struggle on the high plane of
     dignity and discipline. We must not allow our creative protest to
     degenerate into physical violence. Again and again we must rise
     to the majestic heights of meeting physical force with soul
     force. </p>,
     <p>And the marvelous new militarism which has engulfed the Negro
     community must not lead us to a distrust of all white people, for
     many of our white brothers have evidenced by their presence here
     today that they have come to realize that their destiny is part
     of our destiny. </p>,
     <p>So even though we face the difficulties of today and tomorrow
     I still have a dream. It is a dream deeply rooted in the American
     dream. </p>,
     <p>I have a dream that one day this nation will rise up and live
     out the true meaning of its creed: 'We hold these truths to be
     self-evident; that all men are created equal." </p>,
     <p>I have a dream that one day on the red hills of Georgia the
     sons of former slaves and the sons of former slave owners will be
     able to sit together at the table of brotherhood. </p>,
     <p>I have a dream that one day even the state of Mississippi, a
     state sweltering with the heat of injustice, sweltering with the
     heat of oppression, will be transformed into an oasis of freedom
     and justice. </p>,
     <p>I have a dream that little children will one day live in a
     nation where they will not be judged by the color of their skin
     but by the content of their character. </p>,
     <p>I have a dream today. </p>,
     <p>I have a dream that one day down in Alabama, with its vicious
     racists, with its Governor having his lips dripping with the
     words of interposition and nullification, one day right there in
     Alabama little black boys and black girls will be able to join
     hands with little white boys and white girls as sisters and
     brothers. </p>,
     <p>I have a dream today. </p>,
     <p>I have a dream that one day every valley shall be exalted,
     every hill and mountain shall be made low, the rough places
     plains, and the crooked places will be made straight, and before
     the Lord will be revealed, and all flesh shall see it together. </p>,
     <p>This is our hope. This is the faith that I go back to the
     mount with. With this faith we will be able to hew out of the
     mountain of despair a stone of hope. With this faith we will be
     able to transform the genuine discords of our nation into a
     beautiful symphony of brotherhood. With this faith we will be
     able to work together, pray together; to struggle together, to go
     to jail together, to stand up for freedom forever, )mowing that
     we will be free one day. </p>,
     <p>And I say to you today my friends, let freedom ring. From the
     prodigious hilltops of New Hampshire, let freedom ring. From the
     mighty mountains of New York, let freedom ring. From the mighty
     Alleghenies of Pennsylvania! </p>,
     <p>Let freedom ring from the snow capped Rockies of Colorado! </p>,
     <p>Let freedom ring from the curvaceous slopes of California! </p>,
     <p>But not only there; let freedom ring from the Stone Mountain
     of Georgia! </p>,
     <p>Let freedom ring from Lookout Mountain in Tennessee! </p>,
     <p>Let freedom ring from every hill and molehill in Mississippi.
     From every mountainside, let freedom ring. </p>,
     <p>And when this happens, when we allow freedom to ring, when we
     let it ring from every village and hamlet, from every state and
     every city, we will be able to speed up that day when all of
     God's children, black men and white men, Jews and Gentiles,
     Protestants and Catholics, will be able to join hands and sing in
     the words of the old Negro spiritual, "Free at last! Free at
     last! Thank God almighty, we're free at last!" </p>]




```python
#Don't need all the p tags 
```


```python
type(mlkj_speech)
```




    bs4.element.ResultSet




```python
#List comprehension to get rid of the P tags 
```


```python
speech_combined = [p.text for p in mlkj_speech]

print(speech_combined)
```

    ['I am happy to join with you today in what will go down in\r\nhistory as the greatest demonstration for freedom in the history\r\nof our nation. ', 'Five score years ago a great American in whose symbolic shadow\r\nwe stand today signed the Emancipation Proclamation. This\r\nmomentous decree came as a great beckoning light of hope to\r\nmillions of Negro slaves who had been seared in the flames of\r\nwithering injustice. It came as a joyous daybreak to end the long\r\nnight of their captivity. ', 'But one hundred years later the Negro is still not free. One\r\nhundred years later the life of the Negro is still sadly crippled\r\nby the manacles of segregation and the chains of discrimination. ', 'One hundred years later the Negro lives on a lonely island of\r\npoverty in the midst of a vast ocean of material prosperity. ', 'One hundred years later the Negro is still languishing in the\r\ncomers of American society and finds himself in exile in his own\r\nland. ', "We all have come to this hallowed spot to remind America of\r\nthe fierce urgency of now. Now is the time to rise from the dark\r\nand desolate valley of segregation to the sunlit path of racial\r\njustice. Now is the time to change racial injustice to the solid\r\nrock of brotherhood. Now is the time to make justice ring out for\r\nall of God's children. ", 'There will be neither rest nor tranquility in America until\r\nthe Negro is granted citizenship rights. ', 'We must forever conduct our struggle on the high plane of\r\ndignity and discipline. We must not allow our creative protest to\r\ndegenerate into physical violence. Again and again we must rise\r\nto the majestic heights of meeting physical force with soul\r\nforce. ', 'And the marvelous new militarism which has engulfed the Negro\r\ncommunity must not lead us to a distrust of all white people, for\r\nmany of our white brothers have evidenced by their presence here\r\ntoday that they have come to realize that their destiny is part\r\nof our destiny. ', 'So even though we face the difficulties of today and tomorrow\r\nI still have a dream. It is a dream deeply rooted in the American\r\ndream. ', 'I have a dream that one day this nation will rise up and live\r\nout the true meaning of its creed: \'We hold these truths to be\r\nself-evident; that all men are created equal." ', 'I have a dream that one day on the red hills of Georgia the\r\nsons of former slaves and the sons of former slave owners will be\r\nable to sit together at the table of brotherhood. ', 'I have a dream that one day even the state of Mississippi, a\r\nstate sweltering with the heat of injustice, sweltering with the\r\nheat of oppression, will be transformed into an oasis of freedom\r\nand justice. ', 'I have a dream that little children will one day live in a\r\nnation where they will not be judged by the color of their skin\r\nbut by the content of their character. ', 'I have a dream today. ', 'I have a dream that one day down in Alabama, with its vicious\r\nracists, with its Governor having his lips dripping with the\r\nwords of interposition and nullification, one day right there in\r\nAlabama little black boys and black girls will be able to join\r\nhands with little white boys and white girls as sisters and\r\nbrothers. ', 'I have a dream today. ', 'I have a dream that one day every valley shall be exalted,\r\nevery hill and mountain shall be made low, the rough places\r\nplains, and the crooked places will be made straight, and before\r\nthe Lord will be revealed, and all flesh shall see it together. ', 'This is our hope. This is the faith that I go back to the\r\nmount with. With this faith we will be able to hew out of the\r\nmountain of despair a stone of hope. With this faith we will be\r\nable to transform the genuine discords of our nation into a\r\nbeautiful symphony of brotherhood. With this faith we will be\r\nable to work together, pray together; to struggle together, to go\r\nto jail together, to stand up for freedom forever, )mowing that\r\nwe will be free one day. ', 'And I say to you today my friends, let freedom ring. From the\r\nprodigious hilltops of New Hampshire, let freedom ring. From the\r\nmighty mountains of New York, let freedom ring. From the mighty\r\nAlleghenies of Pennsylvania! ', 'Let freedom ring from the snow capped Rockies of Colorado! ', 'Let freedom ring from the curvaceous slopes of California! ', 'But not only there; let freedom ring from the Stone Mountain\r\nof Georgia! ', 'Let freedom ring from Lookout Mountain in Tennessee! ', 'Let freedom ring from every hill and molehill in Mississippi.\r\nFrom every mountainside, let freedom ring. ', 'And when this happens, when we allow freedom to ring, when we\r\nlet it ring from every village and hamlet, from every state and\r\nevery city, we will be able to speed up that day when all of\r\nGod\'s children, black men and white men, Jews and Gentiles,\r\nProtestants and Catholics, will be able to join hands and sing in\r\nthe words of the old Negro spiritual, "Free at last! Free at\r\nlast! Thank God almighty, we\'re free at last!" ']
    


```python
#Speech is separated by commas, \r, \n etc. Remove them next. 
```


```python
type(speech_combined)
```




    list




```python
#Remove sections in speech 
```


```python
' '.join(speech_combined)
```




    'I am happy to join with you today in what will go down in\r\nhistory as the greatest demonstration for freedom in the history\r\nof our nation.  Five score years ago a great American in whose symbolic shadow\r\nwe stand today signed the Emancipation Proclamation. This\r\nmomentous decree came as a great beckoning light of hope to\r\nmillions of Negro slaves who had been seared in the flames of\r\nwithering injustice. It came as a joyous daybreak to end the long\r\nnight of their captivity.  But one hundred years later the Negro is still not free. One\r\nhundred years later the life of the Negro is still sadly crippled\r\nby the manacles of segregation and the chains of discrimination.  One hundred years later the Negro lives on a lonely island of\r\npoverty in the midst of a vast ocean of material prosperity.  One hundred years later the Negro is still languishing in the\r\ncomers of American society and finds himself in exile in his own\r\nland.  We all have come to this hallowed spot to remind America of\r\nthe fierce urgency of now. Now is the time to rise from the dark\r\nand desolate valley of segregation to the sunlit path of racial\r\njustice. Now is the time to change racial injustice to the solid\r\nrock of brotherhood. Now is the time to make justice ring out for\r\nall of God\'s children.  There will be neither rest nor tranquility in America until\r\nthe Negro is granted citizenship rights.  We must forever conduct our struggle on the high plane of\r\ndignity and discipline. We must not allow our creative protest to\r\ndegenerate into physical violence. Again and again we must rise\r\nto the majestic heights of meeting physical force with soul\r\nforce.  And the marvelous new militarism which has engulfed the Negro\r\ncommunity must not lead us to a distrust of all white people, for\r\nmany of our white brothers have evidenced by their presence here\r\ntoday that they have come to realize that their destiny is part\r\nof our destiny.  So even though we face the difficulties of today and tomorrow\r\nI still have a dream. It is a dream deeply rooted in the American\r\ndream.  I have a dream that one day this nation will rise up and live\r\nout the true meaning of its creed: \'We hold these truths to be\r\nself-evident; that all men are created equal."  I have a dream that one day on the red hills of Georgia the\r\nsons of former slaves and the sons of former slave owners will be\r\nable to sit together at the table of brotherhood.  I have a dream that one day even the state of Mississippi, a\r\nstate sweltering with the heat of injustice, sweltering with the\r\nheat of oppression, will be transformed into an oasis of freedom\r\nand justice.  I have a dream that little children will one day live in a\r\nnation where they will not be judged by the color of their skin\r\nbut by the content of their character.  I have a dream today.  I have a dream that one day down in Alabama, with its vicious\r\nracists, with its Governor having his lips dripping with the\r\nwords of interposition and nullification, one day right there in\r\nAlabama little black boys and black girls will be able to join\r\nhands with little white boys and white girls as sisters and\r\nbrothers.  I have a dream today.  I have a dream that one day every valley shall be exalted,\r\nevery hill and mountain shall be made low, the rough places\r\nplains, and the crooked places will be made straight, and before\r\nthe Lord will be revealed, and all flesh shall see it together.  This is our hope. This is the faith that I go back to the\r\nmount with. With this faith we will be able to hew out of the\r\nmountain of despair a stone of hope. With this faith we will be\r\nable to transform the genuine discords of our nation into a\r\nbeautiful symphony of brotherhood. With this faith we will be\r\nable to work together, pray together; to struggle together, to go\r\nto jail together, to stand up for freedom forever, )mowing that\r\nwe will be free one day.  And I say to you today my friends, let freedom ring. From the\r\nprodigious hilltops of New Hampshire, let freedom ring. From the\r\nmighty mountains of New York, let freedom ring. From the mighty\r\nAlleghenies of Pennsylvania!  Let freedom ring from the snow capped Rockies of Colorado!  Let freedom ring from the curvaceous slopes of California!  But not only there; let freedom ring from the Stone Mountain\r\nof Georgia!  Let freedom ring from Lookout Mountain in Tennessee!  Let freedom ring from every hill and molehill in Mississippi.\r\nFrom every mountainside, let freedom ring.  And when this happens, when we allow freedom to ring, when we\r\nlet it ring from every village and hamlet, from every state and\r\nevery city, we will be able to speed up that day when all of\r\nGod\'s children, black men and white men, Jews and Gentiles,\r\nProtestants and Catholics, will be able to join hands and sing in\r\nthe words of the old Negro spiritual, "Free at last! Free at\r\nlast! Thank God almighty, we\'re free at last!" '




```python
string_speech =' '.join(speech_combined)
```


```python
string_speech[:100]
```




    'I am happy to join with you today in what will go down in\r\nhistory as the greatest demonstration for'




```python
#Has bad text, needs to be removed
```


```python
string_speech.replace('\r\n', ' ')
```




    'I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation.  Five score years ago a great American in whose symbolic shadow we stand today signed the Emancipation Proclamation. This momentous decree came as a great beckoning light of hope to millions of Negro slaves who had been seared in the flames of withering injustice. It came as a joyous daybreak to end the long night of their captivity.  But one hundred years later the Negro is still not free. One hundred years later the life of the Negro is still sadly crippled by the manacles of segregation and the chains of discrimination.  One hundred years later the Negro lives on a lonely island of poverty in the midst of a vast ocean of material prosperity.  One hundred years later the Negro is still languishing in the comers of American society and finds himself in exile in his own land.  We all have come to this hallowed spot to remind America of the fierce urgency of now. Now is the time to rise from the dark and desolate valley of segregation to the sunlit path of racial justice. Now is the time to change racial injustice to the solid rock of brotherhood. Now is the time to make justice ring out for all of God\'s children.  There will be neither rest nor tranquility in America until the Negro is granted citizenship rights.  We must forever conduct our struggle on the high plane of dignity and discipline. We must not allow our creative protest to degenerate into physical violence. Again and again we must rise to the majestic heights of meeting physical force with soul force.  And the marvelous new militarism which has engulfed the Negro community must not lead us to a distrust of all white people, for many of our white brothers have evidenced by their presence here today that they have come to realize that their destiny is part of our destiny.  So even though we face the difficulties of today and tomorrow I still have a dream. It is a dream deeply rooted in the American dream.  I have a dream that one day this nation will rise up and live out the true meaning of its creed: \'We hold these truths to be self-evident; that all men are created equal."  I have a dream that one day on the red hills of Georgia the sons of former slaves and the sons of former slave owners will be able to sit together at the table of brotherhood.  I have a dream that one day even the state of Mississippi, a state sweltering with the heat of injustice, sweltering with the heat of oppression, will be transformed into an oasis of freedom and justice.  I have a dream that little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character.  I have a dream today.  I have a dream that one day down in Alabama, with its vicious racists, with its Governor having his lips dripping with the words of interposition and nullification, one day right there in Alabama little black boys and black girls will be able to join hands with little white boys and white girls as sisters and brothers.  I have a dream today.  I have a dream that one day every valley shall be exalted, every hill and mountain shall be made low, the rough places plains, and the crooked places will be made straight, and before the Lord will be revealed, and all flesh shall see it together.  This is our hope. This is the faith that I go back to the mount with. With this faith we will be able to hew out of the mountain of despair a stone of hope. With this faith we will be able to transform the genuine discords of our nation into a beautiful symphony of brotherhood. With this faith we will be able to work together, pray together; to struggle together, to go to jail together, to stand up for freedom forever, )mowing that we will be free one day.  And I say to you today my friends, let freedom ring. From the prodigious hilltops of New Hampshire, let freedom ring. From the mighty mountains of New York, let freedom ring. From the mighty Alleghenies of Pennsylvania!  Let freedom ring from the snow capped Rockies of Colorado!  Let freedom ring from the curvaceous slopes of California!  But not only there; let freedom ring from the Stone Mountain of Georgia!  Let freedom ring from Lookout Mountain in Tennessee!  Let freedom ring from every hill and molehill in Mississippi. From every mountainside, let freedom ring.  And when this happens, when we allow freedom to ring, when we let it ring from every village and hamlet, from every state and every city, we will be able to speed up that day when all of God\'s children, black men and white men, Jews and Gentiles, Protestants and Catholics, will be able to join hands and sing in the words of the old Negro spiritual, "Free at last! Free at last! Thank God almighty, we\'re free at last!" '




```python
#Get rid of the \s 
```


```python
string_speech_cleaned = string_speech.replace('\r\n', ' ')
```


```python
string_speech_cleaned
```




    'I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation.  Five score years ago a great American in whose symbolic shadow we stand today signed the Emancipation Proclamation. This momentous decree came as a great beckoning light of hope to millions of Negro slaves who had been seared in the flames of withering injustice. It came as a joyous daybreak to end the long night of their captivity.  But one hundred years later the Negro is still not free. One hundred years later the life of the Negro is still sadly crippled by the manacles of segregation and the chains of discrimination.  One hundred years later the Negro lives on a lonely island of poverty in the midst of a vast ocean of material prosperity.  One hundred years later the Negro is still languishing in the comers of American society and finds himself in exile in his own land.  We all have come to this hallowed spot to remind America of the fierce urgency of now. Now is the time to rise from the dark and desolate valley of segregation to the sunlit path of racial justice. Now is the time to change racial injustice to the solid rock of brotherhood. Now is the time to make justice ring out for all of God\'s children.  There will be neither rest nor tranquility in America until the Negro is granted citizenship rights.  We must forever conduct our struggle on the high plane of dignity and discipline. We must not allow our creative protest to degenerate into physical violence. Again and again we must rise to the majestic heights of meeting physical force with soul force.  And the marvelous new militarism which has engulfed the Negro community must not lead us to a distrust of all white people, for many of our white brothers have evidenced by their presence here today that they have come to realize that their destiny is part of our destiny.  So even though we face the difficulties of today and tomorrow I still have a dream. It is a dream deeply rooted in the American dream.  I have a dream that one day this nation will rise up and live out the true meaning of its creed: \'We hold these truths to be self-evident; that all men are created equal."  I have a dream that one day on the red hills of Georgia the sons of former slaves and the sons of former slave owners will be able to sit together at the table of brotherhood.  I have a dream that one day even the state of Mississippi, a state sweltering with the heat of injustice, sweltering with the heat of oppression, will be transformed into an oasis of freedom and justice.  I have a dream that little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character.  I have a dream today.  I have a dream that one day down in Alabama, with its vicious racists, with its Governor having his lips dripping with the words of interposition and nullification, one day right there in Alabama little black boys and black girls will be able to join hands with little white boys and white girls as sisters and brothers.  I have a dream today.  I have a dream that one day every valley shall be exalted, every hill and mountain shall be made low, the rough places plains, and the crooked places will be made straight, and before the Lord will be revealed, and all flesh shall see it together.  This is our hope. This is the faith that I go back to the mount with. With this faith we will be able to hew out of the mountain of despair a stone of hope. With this faith we will be able to transform the genuine discords of our nation into a beautiful symphony of brotherhood. With this faith we will be able to work together, pray together; to struggle together, to go to jail together, to stand up for freedom forever, )mowing that we will be free one day.  And I say to you today my friends, let freedom ring. From the prodigious hilltops of New Hampshire, let freedom ring. From the mighty mountains of New York, let freedom ring. From the mighty Alleghenies of Pennsylvania!  Let freedom ring from the snow capped Rockies of Colorado!  Let freedom ring from the curvaceous slopes of California!  But not only there; let freedom ring from the Stone Mountain of Georgia!  Let freedom ring from Lookout Mountain in Tennessee!  Let freedom ring from every hill and molehill in Mississippi. From every mountainside, let freedom ring.  And when this happens, when we allow freedom to ring, when we let it ring from every village and hamlet, from every state and every city, we will be able to speed up that day when all of God\'s children, black men and white men, Jews and Gentiles, Protestants and Catholics, will be able to join hands and sing in the words of the old Negro spiritual, "Free at last! Free at last! Thank God almighty, we\'re free at last!" '




```python
string_speech_cleaned.replace('\\',' ')
```




    'I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation.  Five score years ago a great American in whose symbolic shadow we stand today signed the Emancipation Proclamation. This momentous decree came as a great beckoning light of hope to millions of Negro slaves who had been seared in the flames of withering injustice. It came as a joyous daybreak to end the long night of their captivity.  But one hundred years later the Negro is still not free. One hundred years later the life of the Negro is still sadly crippled by the manacles of segregation and the chains of discrimination.  One hundred years later the Negro lives on a lonely island of poverty in the midst of a vast ocean of material prosperity.  One hundred years later the Negro is still languishing in the comers of American society and finds himself in exile in his own land.  We all have come to this hallowed spot to remind America of the fierce urgency of now. Now is the time to rise from the dark and desolate valley of segregation to the sunlit path of racial justice. Now is the time to change racial injustice to the solid rock of brotherhood. Now is the time to make justice ring out for all of God\'s children.  There will be neither rest nor tranquility in America until the Negro is granted citizenship rights.  We must forever conduct our struggle on the high plane of dignity and discipline. We must not allow our creative protest to degenerate into physical violence. Again and again we must rise to the majestic heights of meeting physical force with soul force.  And the marvelous new militarism which has engulfed the Negro community must not lead us to a distrust of all white people, for many of our white brothers have evidenced by their presence here today that they have come to realize that their destiny is part of our destiny.  So even though we face the difficulties of today and tomorrow I still have a dream. It is a dream deeply rooted in the American dream.  I have a dream that one day this nation will rise up and live out the true meaning of its creed: \'We hold these truths to be self-evident; that all men are created equal."  I have a dream that one day on the red hills of Georgia the sons of former slaves and the sons of former slave owners will be able to sit together at the table of brotherhood.  I have a dream that one day even the state of Mississippi, a state sweltering with the heat of injustice, sweltering with the heat of oppression, will be transformed into an oasis of freedom and justice.  I have a dream that little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character.  I have a dream today.  I have a dream that one day down in Alabama, with its vicious racists, with its Governor having his lips dripping with the words of interposition and nullification, one day right there in Alabama little black boys and black girls will be able to join hands with little white boys and white girls as sisters and brothers.  I have a dream today.  I have a dream that one day every valley shall be exalted, every hill and mountain shall be made low, the rough places plains, and the crooked places will be made straight, and before the Lord will be revealed, and all flesh shall see it together.  This is our hope. This is the faith that I go back to the mount with. With this faith we will be able to hew out of the mountain of despair a stone of hope. With this faith we will be able to transform the genuine discords of our nation into a beautiful symphony of brotherhood. With this faith we will be able to work together, pray together; to struggle together, to go to jail together, to stand up for freedom forever, )mowing that we will be free one day.  And I say to you today my friends, let freedom ring. From the prodigious hilltops of New Hampshire, let freedom ring. From the mighty mountains of New York, let freedom ring. From the mighty Alleghenies of Pennsylvania!  Let freedom ring from the snow capped Rockies of Colorado!  Let freedom ring from the curvaceous slopes of California!  But not only there; let freedom ring from the Stone Mountain of Georgia!  Let freedom ring from Lookout Mountain in Tennessee!  Let freedom ring from every hill and molehill in Mississippi. From every mountainside, let freedom ring.  And when this happens, when we allow freedom to ring, when we let it ring from every village and hamlet, from every state and every city, we will be able to speed up that day when all of God\'s children, black men and white men, Jews and Gentiles, Protestants and Catholics, will be able to join hands and sing in the words of the old Negro spiritual, "Free at last! Free at last! Thank God almighty, we\'re free at last!" '




```python
# Backslashes are still there when cleaning up 
```


```python
# Solution: Get rid of the punctuation?? 
```


```python
import re
```


```python
# Write regular expression to remove punctuation
```


```python
re.sub(r'[\w\s]','', string_speech_cleaned)
```




    '...........\'.....,...:\'-;.".,,,...,,,..,,,,,.....,;,,,).,.,.,.!!!;!!.,.,,,,\',,,,,"!!,\'!"'




```python
speech_no_punct = re.sub(r'[\w\s]','', string_speech_cleaned)

print(speech_no_punct)
```

    ...........'.....,...:'-;.".,,,...,,,..,,,,,.....,;,,,).,.,.,.!!!;!!.,.,,,,',,,,,"!!,'!"
    


```python
speech_no_punct = re.sub(r'[^\w\s]','', string_speech_cleaned)  
```


```python
print(speech_no_punct)
```

    I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation  Five score years ago a great American in whose symbolic shadow we stand today signed the Emancipation Proclamation This momentous decree came as a great beckoning light of hope to millions of Negro slaves who had been seared in the flames of withering injustice It came as a joyous daybreak to end the long night of their captivity  But one hundred years later the Negro is still not free One hundred years later the life of the Negro is still sadly crippled by the manacles of segregation and the chains of discrimination  One hundred years later the Negro lives on a lonely island of poverty in the midst of a vast ocean of material prosperity  One hundred years later the Negro is still languishing in the comers of American society and finds himself in exile in his own land  We all have come to this hallowed spot to remind America of the fierce urgency of now Now is the time to rise from the dark and desolate valley of segregation to the sunlit path of racial justice Now is the time to change racial injustice to the solid rock of brotherhood Now is the time to make justice ring out for all of Gods children  There will be neither rest nor tranquility in America until the Negro is granted citizenship rights  We must forever conduct our struggle on the high plane of dignity and discipline We must not allow our creative protest to degenerate into physical violence Again and again we must rise to the majestic heights of meeting physical force with soul force  And the marvelous new militarism which has engulfed the Negro community must not lead us to a distrust of all white people for many of our white brothers have evidenced by their presence here today that they have come to realize that their destiny is part of our destiny  So even though we face the difficulties of today and tomorrow I still have a dream It is a dream deeply rooted in the American dream  I have a dream that one day this nation will rise up and live out the true meaning of its creed We hold these truths to be selfevident that all men are created equal  I have a dream that one day on the red hills of Georgia the sons of former slaves and the sons of former slave owners will be able to sit together at the table of brotherhood  I have a dream that one day even the state of Mississippi a state sweltering with the heat of injustice sweltering with the heat of oppression will be transformed into an oasis of freedom and justice  I have a dream that little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character  I have a dream today  I have a dream that one day down in Alabama with its vicious racists with its Governor having his lips dripping with the words of interposition and nullification one day right there in Alabama little black boys and black girls will be able to join hands with little white boys and white girls as sisters and brothers  I have a dream today  I have a dream that one day every valley shall be exalted every hill and mountain shall be made low the rough places plains and the crooked places will be made straight and before the Lord will be revealed and all flesh shall see it together  This is our hope This is the faith that I go back to the mount with With this faith we will be able to hew out of the mountain of despair a stone of hope With this faith we will be able to transform the genuine discords of our nation into a beautiful symphony of brotherhood With this faith we will be able to work together pray together to struggle together to go to jail together to stand up for freedom forever mowing that we will be free one day  And I say to you today my friends let freedom ring From the prodigious hilltops of New Hampshire let freedom ring From the mighty mountains of New York let freedom ring From the mighty Alleghenies of Pennsylvania  Let freedom ring from the snow capped Rockies of Colorado  Let freedom ring from the curvaceous slopes of California  But not only there let freedom ring from the Stone Mountain of Georgia  Let freedom ring from Lookout Mountain in Tennessee  Let freedom ring from every hill and molehill in Mississippi From every mountainside let freedom ring  And when this happens when we allow freedom to ring when we let it ring from every village and hamlet from every state and every city we will be able to speed up that day when all of Gods children black men and white men Jews and Gentiles Protestants and Catholics will be able to join hands and sing in the words of the old Negro spiritual Free at last Free at last Thank God almighty were free at last 
    


```python
# Run counts on speech 
```


```python
speech_lower = speech_no_punct.lower()
```


```python
#Split Method: Split based on white space 
```


```python
re.split(r'\s+', speech_lower) 
```




    ['i',
     'am',
     'happy',
     'to',
     'join',
     'with',
     'you',
     'today',
     'in',
     'what',
     'will',
     'go',
     'down',
     'in',
     'history',
     'as',
     'the',
     'greatest',
     'demonstration',
     'for',
     'freedom',
     'in',
     'the',
     'history',
     'of',
     'our',
     'nation',
     'five',
     'score',
     'years',
     'ago',
     'a',
     'great',
     'american',
     'in',
     'whose',
     'symbolic',
     'shadow',
     'we',
     'stand',
     'today',
     'signed',
     'the',
     'emancipation',
     'proclamation',
     'this',
     'momentous',
     'decree',
     'came',
     'as',
     'a',
     'great',
     'beckoning',
     'light',
     'of',
     'hope',
     'to',
     'millions',
     'of',
     'negro',
     'slaves',
     'who',
     'had',
     'been',
     'seared',
     'in',
     'the',
     'flames',
     'of',
     'withering',
     'injustice',
     'it',
     'came',
     'as',
     'a',
     'joyous',
     'daybreak',
     'to',
     'end',
     'the',
     'long',
     'night',
     'of',
     'their',
     'captivity',
     'but',
     'one',
     'hundred',
     'years',
     'later',
     'the',
     'negro',
     'is',
     'still',
     'not',
     'free',
     'one',
     'hundred',
     'years',
     'later',
     'the',
     'life',
     'of',
     'the',
     'negro',
     'is',
     'still',
     'sadly',
     'crippled',
     'by',
     'the',
     'manacles',
     'of',
     'segregation',
     'and',
     'the',
     'chains',
     'of',
     'discrimination',
     'one',
     'hundred',
     'years',
     'later',
     'the',
     'negro',
     'lives',
     'on',
     'a',
     'lonely',
     'island',
     'of',
     'poverty',
     'in',
     'the',
     'midst',
     'of',
     'a',
     'vast',
     'ocean',
     'of',
     'material',
     'prosperity',
     'one',
     'hundred',
     'years',
     'later',
     'the',
     'negro',
     'is',
     'still',
     'languishing',
     'in',
     'the',
     'comers',
     'of',
     'american',
     'society',
     'and',
     'finds',
     'himself',
     'in',
     'exile',
     'in',
     'his',
     'own',
     'land',
     'we',
     'all',
     'have',
     'come',
     'to',
     'this',
     'hallowed',
     'spot',
     'to',
     'remind',
     'america',
     'of',
     'the',
     'fierce',
     'urgency',
     'of',
     'now',
     'now',
     'is',
     'the',
     'time',
     'to',
     'rise',
     'from',
     'the',
     'dark',
     'and',
     'desolate',
     'valley',
     'of',
     'segregation',
     'to',
     'the',
     'sunlit',
     'path',
     'of',
     'racial',
     'justice',
     'now',
     'is',
     'the',
     'time',
     'to',
     'change',
     'racial',
     'injustice',
     'to',
     'the',
     'solid',
     'rock',
     'of',
     'brotherhood',
     'now',
     'is',
     'the',
     'time',
     'to',
     'make',
     'justice',
     'ring',
     'out',
     'for',
     'all',
     'of',
     'gods',
     'children',
     'there',
     'will',
     'be',
     'neither',
     'rest',
     'nor',
     'tranquility',
     'in',
     'america',
     'until',
     'the',
     'negro',
     'is',
     'granted',
     'citizenship',
     'rights',
     'we',
     'must',
     'forever',
     'conduct',
     'our',
     'struggle',
     'on',
     'the',
     'high',
     'plane',
     'of',
     'dignity',
     'and',
     'discipline',
     'we',
     'must',
     'not',
     'allow',
     'our',
     'creative',
     'protest',
     'to',
     'degenerate',
     'into',
     'physical',
     'violence',
     'again',
     'and',
     'again',
     'we',
     'must',
     'rise',
     'to',
     'the',
     'majestic',
     'heights',
     'of',
     'meeting',
     'physical',
     'force',
     'with',
     'soul',
     'force',
     'and',
     'the',
     'marvelous',
     'new',
     'militarism',
     'which',
     'has',
     'engulfed',
     'the',
     'negro',
     'community',
     'must',
     'not',
     'lead',
     'us',
     'to',
     'a',
     'distrust',
     'of',
     'all',
     'white',
     'people',
     'for',
     'many',
     'of',
     'our',
     'white',
     'brothers',
     'have',
     'evidenced',
     'by',
     'their',
     'presence',
     'here',
     'today',
     'that',
     'they',
     'have',
     'come',
     'to',
     'realize',
     'that',
     'their',
     'destiny',
     'is',
     'part',
     'of',
     'our',
     'destiny',
     'so',
     'even',
     'though',
     'we',
     'face',
     'the',
     'difficulties',
     'of',
     'today',
     'and',
     'tomorrow',
     'i',
     'still',
     'have',
     'a',
     'dream',
     'it',
     'is',
     'a',
     'dream',
     'deeply',
     'rooted',
     'in',
     'the',
     'american',
     'dream',
     'i',
     'have',
     'a',
     'dream',
     'that',
     'one',
     'day',
     'this',
     'nation',
     'will',
     'rise',
     'up',
     'and',
     'live',
     'out',
     'the',
     'true',
     'meaning',
     'of',
     'its',
     'creed',
     'we',
     'hold',
     'these',
     'truths',
     'to',
     'be',
     'selfevident',
     'that',
     'all',
     'men',
     'are',
     'created',
     'equal',
     'i',
     'have',
     'a',
     'dream',
     'that',
     'one',
     'day',
     'on',
     'the',
     'red',
     'hills',
     'of',
     'georgia',
     'the',
     'sons',
     'of',
     'former',
     'slaves',
     'and',
     'the',
     'sons',
     'of',
     'former',
     'slave',
     'owners',
     'will',
     'be',
     'able',
     'to',
     'sit',
     'together',
     'at',
     'the',
     'table',
     'of',
     'brotherhood',
     'i',
     'have',
     'a',
     'dream',
     'that',
     'one',
     'day',
     'even',
     'the',
     'state',
     'of',
     'mississippi',
     'a',
     'state',
     'sweltering',
     'with',
     'the',
     'heat',
     'of',
     'injustice',
     'sweltering',
     'with',
     'the',
     'heat',
     'of',
     'oppression',
     'will',
     'be',
     'transformed',
     'into',
     'an',
     'oasis',
     'of',
     'freedom',
     'and',
     'justice',
     'i',
     'have',
     'a',
     'dream',
     'that',
     'little',
     'children',
     'will',
     'one',
     'day',
     'live',
     'in',
     'a',
     'nation',
     'where',
     'they',
     'will',
     'not',
     'be',
     'judged',
     'by',
     'the',
     'color',
     'of',
     'their',
     'skin',
     'but',
     'by',
     'the',
     'content',
     'of',
     'their',
     'character',
     'i',
     'have',
     'a',
     'dream',
     'today',
     'i',
     'have',
     'a',
     'dream',
     'that',
     'one',
     'day',
     'down',
     'in',
     'alabama',
     'with',
     'its',
     'vicious',
     'racists',
     'with',
     'its',
     'governor',
     'having',
     'his',
     'lips',
     'dripping',
     'with',
     'the',
     'words',
     'of',
     'interposition',
     'and',
     'nullification',
     'one',
     'day',
     'right',
     'there',
     'in',
     'alabama',
     'little',
     'black',
     'boys',
     'and',
     'black',
     'girls',
     'will',
     'be',
     'able',
     'to',
     'join',
     'hands',
     'with',
     'little',
     'white',
     'boys',
     'and',
     'white',
     'girls',
     'as',
     'sisters',
     'and',
     'brothers',
     'i',
     'have',
     'a',
     'dream',
     'today',
     'i',
     'have',
     'a',
     'dream',
     'that',
     'one',
     'day',
     'every',
     'valley',
     'shall',
     'be',
     'exalted',
     'every',
     'hill',
     'and',
     'mountain',
     'shall',
     'be',
     'made',
     'low',
     'the',
     'rough',
     'places',
     'plains',
     'and',
     'the',
     'crooked',
     'places',
     'will',
     'be',
     'made',
     'straight',
     'and',
     'before',
     'the',
     'lord',
     'will',
     'be',
     'revealed',
     'and',
     'all',
     'flesh',
     'shall',
     'see',
     'it',
     'together',
     'this',
     'is',
     'our',
     'hope',
     'this',
     'is',
     'the',
     'faith',
     'that',
     'i',
     'go',
     'back',
     'to',
     'the',
     'mount',
     'with',
     'with',
     'this',
     'faith',
     'we',
     'will',
     'be',
     'able',
     'to',
     'hew',
     'out',
     'of',
     'the',
     'mountain',
     'of',
     'despair',
     'a',
     'stone',
     'of',
     'hope',
     'with',
     'this',
     'faith',
     'we',
     'will',
     'be',
     'able',
     'to',
     'transform',
     'the',
     'genuine',
     'discords',
     'of',
     'our',
     'nation',
     'into',
     'a',
     'beautiful',
     'symphony',
     'of',
     'brotherhood',
     'with',
     'this',
     'faith',
     'we',
     'will',
     'be',
     'able',
     'to',
     'work',
     'together',
     'pray',
     'together',
     'to',
     'struggle',
     'together',
     'to',
     'go',
     'to',
     'jail',
     'together',
     'to',
     'stand',
     'up',
     'for',
     'freedom',
     'forever',
     'mowing',
     'that',
     'we',
     'will',
     'be',
     'free',
     'one',
     'day',
     'and',
     'i',
     'say',
     'to',
     'you',
     'today',
     'my',
     'friends',
     'let',
     'freedom',
     'ring',
     'from',
     'the',
     'prodigious',
     'hilltops',
     'of',
     'new',
     'hampshire',
     'let',
     'freedom',
     'ring',
     'from',
     'the',
     'mighty',
     'mountains',
     'of',
     'new',
     'york',
     'let',
     'freedom',
     'ring',
     'from',
     'the',
     'mighty',
     'alleghenies',
     'of',
     'pennsylvania',
     'let',
     'freedom',
     'ring',
     'from',
     'the',
     'snow',
     'capped',
     'rockies',
     'of',
     'colorado',
     'let',
     'freedom',
     'ring',
     'from',
     'the',
     'curvaceous',
     'slopes',
     'of',
     'california',
     'but',
     'not',
     'only',
     'there',
     'let',
     'freedom',
     'ring',
     'from',
     'the',
     'stone',
     'mountain',
     'of',
     'georgia',
     'let',
     'freedom',
     'ring',
     'from',
     'lookout',
     'mountain',
     'in',
     'tennessee',
     'let',
     'freedom',
     'ring',
     'from',
     'every',
     'hill',
     'and',
     'molehill',
     'in',
     'mississippi',
     'from',
     'every',
     'mountainside',
     'let',
     'freedom',
     'ring',
     'and',
     'when',
     'this',
     'happens',
     'when',
     'we',
     'allow',
     'freedom',
     'to',
     'ring',
     'when',
     'we',
     'let',
     'it',
     'ring',
     'from',
     'every',
     'village',
     'and',
     'hamlet',
     'from',
     'every',
     'state',
     'and',
     'every',
     'city',
     'we',
     'will',
     'be',
     'able',
     'to',
     'speed',
     'up',
     'that',
     'day',
     'when',
     'all',
     'of',
     'gods',
     'children',
     'black',
     'men',
     'and',
     'white',
     'men',
     'jews',
     'and',
     'gentiles',
     'protestants',
     'and',
     'catholics',
     'will',
     'be',
     'able',
     'to',
     'join',
     'hands',
     'and',
     'sing',
     'in',
     'the',
     'words',
     'of',
     'the',
     'old',
     'negro',
     'spiritual',
     'free',
     'at',
     'last',
     'free',
     'at',
     'last',
     'thank',
     'god',
     'almighty',
     'were',
     'free',
     'at',
     'last',
     '']




```python
speech_broken_out = re.split(r'\s+', speech_lower) 
```


```python
import pandas as pd 
```


```python
df = pd.DataFrame(speech_broken_out).value_counts()     #runs a count on it 
```


```python
df
```




    0      
    the        54
    of         49
    to         29
    and        27
    a          20
               ..
    jews        1
    joyous      1
    judged      1
    land        1
    lookout     1
    Name: count, Length: 323, dtype: int64




```python
#Export to Excel 

df.to_csv(r'C:\Users\tayab\Documents\Data Projects\Analyst Builder\Python Project\MLK_Speech_Counts.csv', header = ['Counts'], index_label =['Word'] )
```


```python

```
