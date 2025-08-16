using { /Fortnite.com/Devices }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Game }
using { /Verse.org/Simulation }
using { /UnrealEngine.com/Temporary/Diagnostics }


HelicopterScript := class(creative_device):
    @editable Helicopter_Prop : creative_prop = creative_prop{}
    @editable Helicopter_Spawner : vehicle_spawner_helicopter_device = vehicle_spawner_helicopter_device{}

    @editable DeliverComponents_Zone : mutator_zone_device = mutator_zone_device{}
    @editable Helicopter_Components : []carryable_spawner_device = array{}
    @editable PlayerManager : Player_Manager = Player_Manager{}




    var HelicopterComponentCollectedByAgent : [agent]string = map{}
    var InitializedMaps : logic = false
    
    var InsertedComponentsInHelicopter : [string]logic = map{
        "Repulsor_A" => false, 
        "Repulsor_B" => false, 
        "Main_Propellers" => false, 
        "Secondary_Propellers" => false,
        "Energy" => false
    }








    OnBegin<override>()<suspends>:void=
        if(InitializedMaps = false):#If maps haven't been initialized yet, initialize them.
            InitializePlayersMaps()
            set InitializedMaps = true




        if:#When one of the components gets collected, "HelicopterComponentCollectedByAgent" gets set with the component name
            Repulsor_A := Helicopter_Components[0]
            Repulsor_B := Helicopter_Components[1]
            Main_Propellers := Helicopter_Components[2]
            Secondary_Propellers := Helicopter_Components[3]


        then:
            Repulsor_A.PickUpEvent.Subscribe(When_RepulsorA_GetsCollected)
            Repulsor_B.PickUpEvent.Subscribe(When_RepulsorB_GetsCollected)
            Main_Propellers.PickUpEvent.Subscribe(When_MainPropellers_GetsCollected)
            Secondary_Propellers.PickUpEvent.Subscribe(When_SecondaryPropellers_GetsCollected)
        



        DeliverComponents_Zone.AgentEntersEvent.Subscribe(WhenPlayerInsertsComponent)






            
    WhenPlayerInsertsComponent(Agent:agent):void=
        if(not HelicopterComponentCollectedByAgent[Agent] = "None"):#If the "HelicopterComponentCollectedByAgent" map is different than "None", the component gets applied to the helicopter prop
            if:#This "IF" statement changes the materials inside the "Helicopter_Prop"

                #DEVICES THAT WILL BE USED AFTER THIS "IF" STATEMENT!!!
                Repulsor_A := Helicopter_Components[0]
                Repulsor_B := Helicopter_Components[1]
                Main_Propellers := Helicopter_Components[2]
                Secondary_Propellers := Helicopter_Components[3]
                Energy_Bottle := Helicopter_Components[4]




                case(HelicopterComponentCollectedByAgent[Agent]):#Checks what component is currently possessed by the player | NOTE: "Materials" is the folder's name inside the Editor. It contains the helicopter material
                    "Repulsor_A" =>    
                        Helicopter_Prop.SetMaterial(Materials.Hoagie_Part, ?Index := 2)    
                        if:
                            set InsertedComponentsInHelicopter["Repulsor_A"] = true



                    "Repulsor_B" =>
                        Helicopter_Prop.SetMaterial(Materials.Hoagie_Part, ?Index := 5) 
                        if:
                            set InsertedComponentsInHelicopter["Repulsor_B"] = true

    
                    "Main_Propellers" =>
                        Helicopter_Prop.SetMaterial(Materials.Hoagie_Part, ?Index := 4) 
                        if:
                            set InsertedComponentsInHelicopter["Main_Propellers"] = true
                            



                    "Secondary_Propellers" =>
                        Helicopter_Prop.SetMaterial(Materials.Hoagie_Part, ?Index := 6) 
                        if:
                            set InsertedComponentsInHelicopter["Secondary_Propellers"] = true




                    "Energy" =>
                        if:
                            set InsertedComponentsInHelicopter["Energy"] = true        




            then:#Destroys the Carryable Object held by the player
                if(HelicopterComponentCollectedByAgent[Agent] = "Repulsor_A"):
                    Repulsor_A.Explode()


                else if(HelicopterComponentCollectedByAgent[Agent] = "Repulsor_B"):
                    Repulsor_B.Explode()


                else if(HelicopterComponentCollectedByAgent[Agent] = "Main_Propellers"):
                    Main_Propellers.Explode()


                else if(HelicopterComponentCollectedByAgent[Agent] = "Secondary_Propellers"):
                    Secondary_Propellers.Explode()

                else if(HelicopterComponentCollectedByAgent[Agent] = "Energy"):
                    Energy_Bottle.Explode()



                
                if(set HelicopterComponentCollectedByAgent[Agent] = "None"){}#Resets the "HelicopterComponentCollectedByAgent" map
                



                if:#If all the components have been inserted into the helicopter, then it spawns the actual one
                    InsertedComponentsInHelicopter["Repulsor_A"] = true
                    InsertedComponentsInHelicopter["Repulsor_B"] = true
                    InsertedComponentsInHelicopter["Main_Propellers"] = true
                    InsertedComponentsInHelicopter["Secondary_Propellers"] = true
                    InsertedComponentsInHelicopter["Energy"] = true

                then:
                    Helicopter_Prop.Dispose()
                    DeliverComponents_Zone.Disable()
                    Helicopter_Spawner.Enable()






    When_RepulsorA_GetsCollected(Agent:agent):void=
        if:
            set HelicopterComponentCollectedByAgent[Agent] = "Repulsor_A"
            
    When_RepulsorB_GetsCollected(Agent:agent):void=
        if:
            set HelicopterComponentCollectedByAgent[Agent] = "Repulsor_B" 

    When_MainPropellers_GetsCollected(Agent:agent):void=
        if:
            set HelicopterComponentCollectedByAgent[Agent] = "Main_Propellers"

    When_SecondaryPropellers_GetsCollected(Agent:agent):void=
        if:
            set HelicopterComponentCollectedByAgent[Agent] = "Secondary_Propellers"
            
    When_Energy_GetsCollected(Agent:agent):void=
        if:
            Player := player[Agent]
            Energy_Bottle := Helicopter_Components[4]
            set HelicopterComponentCollectedByAgent[Agent] = "Energy"

        then:
            Energy_Bottle.ForcePlayerToCarry(Player)










    InitializePlayersMaps():void=
        var Players : []player = PlayerManager.RetrievePlayersList()


        for(Player:Players):#This "For" statement sets the players "HelicopterComponentCollectedByAgent" map to the default value
            if:
                HelicopterComponentCollectedByAgent[Player] = "None"
