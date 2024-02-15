#replay  #code

Replays game events like betting, games, etc. 
Uses Velocity (similar to thymeleaf) to produce generic configurable html to reproduce last play of a game using the informaiton relevant for that point in time. 

Processor for the replay functionality is configured through the databases using a plugin-like/reflexion mechanism. (good lord...) RemoteGameDAO can be used for tracking this logic. 


it can be accesed through getHTMLReplayInfo(AbstractReplayProcessor), retrieves replay information as dto, converts it to xml, and afterwards turns tha tinto html . 