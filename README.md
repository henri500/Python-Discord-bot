# Python-Discord-bot
# Project brief:
By the end of this prototype, the chatbot has the following features:
- Stream music from youtube in to the discord chat channel they are currently in
- Find navigation routes to place users want
- Provide news headlines concerning sports and more from different sources depending on the user's choice
- Give information on sport team such as foundation date, competion,country and  the color of the team's kit


# What did i do ?
In this project, apart from helping my team membes with some coding problems I was in charge of the following tasks:

- Create the interface between the discord API and the main script of the chatbot
- Handle message recieved from users and determine what action the chatbot would do. An example of this is how I filter commands from common text.
- Used OpenWeather API to retrieve weather information accordin to the user's location.

# How does it work ?
The module requirements for the chatbot wok are listed in the "Requirement.txt" file of this repository.
Because we wanted the chatbot's main interface to be discord, we had to import it and create a  dicord client object as such :
      
      TESS=discord.Client() #--where  TESS is the client object that we create.
      TESS.run()            #--Using the discord run function that connects the machine running the scripts to the discord server.
                            #--This run fucntion is placed at the end of the script.
Now that the bot is up and running, We used the *@Client.event* functtion to detect incoming messages. To be able to differentiate if the text reieved what a command or general text i wrote the followig code:

      if ((message.content[0])=='!' and ('play' in message.content)): #--checking if an input is a command

            if TESS.is_voice_connected(server) == False:              #--checking if we already have a voice connection to the voice client 
                  await TESS.join_voice_channel(channel)
                  TESS_voice=TESS.voice_client_in(server)
                  print('joined voice channel')
                  message.content=message.content.strip('!')
                  message.content=message.content.strip('play')
                  first_link=get_vid_link(message.content)
                  song_lenght=int(lenght_song(first_link))
                  vid='https://youtube.com{}'.format(first_link)
                  song_player=await TESS_voice.create_ytdl_player(vid) #--Creates a stream player in a new thread in  the backgrounf from youtube.
                  players_instances[server.id]=song_player             #-- Storing an instance of the song play so that it can accessed later
                  song_player.start()
                  print(players_instances)
            else:
                  TESS_voice=TESS.voice_client_in(server)
                  message.content=message.content.strip('!')
                  message.content=message.content.strip('play')
                  message.content=format_message(message.content)
                  first_link=get_vid_link(message.content)
                  song_lenght=int(lenght_song(first_link))
                  vid='https://youtube.com{}'.format(first_link)
                  song_player=await TESS_voice.create_ytdl_player(vid)
                  players_instances[server.id]=song_player
                  song_player.start()

In the above example, if the first character of the in-comming message is '!' and if it contains the string 'play',then I consider this message to be a command. In this case, the command is to play a song. I used the same method to identify other commands such as stop and resume. Now that I knmow the message is a "play <song>" command,.I checked if the theres was a voice connection between the user and the bot in other to stream audio to the channel the user is in. I removed the command prefix("!" and "play") from the message  and passed it to the *format_message* function which remove charaters such as question marks.
in order to play the corect song required by the user, I wrote a *get_vid_link* function that uses requests and BeautifulSoup modules to search for a song on youtube and returns the id of th first e video that appears onn a youtube search.
 
__**why does it return onmly the first link?**__ Well based on youtube's searching algorithm which is very accurate, the first link on the page would very likely be the song or artist most popular song(this will be the case if the user ony enters the name of an artist.).
This can of course be improved in later prototypes bye giving the choice to the user to select between the first five results returned by the youtube search engine.
    
      
      
      
      
 






# What I have learnt from this project:
Throught out the course of this project I have gained many valuable skills. These include




# Project evaluation:























*The link to the main project repository  with all the code is fond at https://github.coventry.ac.uk/demanouh/CHATBOT*
https://guides.github.com/features/mastering-markdown/
