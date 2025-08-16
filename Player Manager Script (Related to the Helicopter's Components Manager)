
using { /Fortnite.com/Devices }
using { /Fortnite.com/Game }
using { /Fortnite.com/Characters }
using { /Verse.org/Simulation }
using { /UnrealEngine.com/Temporary/Diagnostics }


Player_Manager := class(creative_device):
    var Players : []player = array{}
    var InitializedPlayers : logic = false


    OnBegin<override>()<suspends>:void=
        if(InitializedPlayers = false):#If the players list hasn't been initialized, it initalizes it
            InitializePlayersList()
            set InitializedPlayers = true  
        
        
        #When a player Joins/Leaves the game, the Players list gets updated
        GetPlayspace().PlayerAddedEvent().Subscribe(UpdatePlayersList)
        GetPlayspace().PlayerRemovedEvent().Subscribe(UpdatePlayersList)







    RetrievePlayersList():[]player=#If called, this function returns the current players list
        return Players








    InitializePlayersList():void=
        set Players = GetPlayspace().GetPlayers()
    UpdatePlayersList(Player:player):void=
        set Players = GetPlayspace().GetPlayers()
