# FNAF-Text-Version-
### - Notes - ###

# -- CAM List -- #

# 1A = Show Stage
# 1B = Dining Area
# 1C = Pirate Cove
# 2A = West Hall
# 2B = West Hall Corner
# 3 = Supply Closet
# 4A = East Hall
# 4B = East Hall Corner
# 5 = Backstage
# 6 = Kitchen (audio only)
# 7 = Bathroom

### - End Notes - ###


### - Pre-Game Setup - ###

from random import *  # Allows for animatronic movement and GF randomisation

camlist = ["cam 1A", "cam 1B", "cam 1C", "cam 2A", "cam 2B", "cam 3", "cam 4A", "cam 4B", "cam 5", "cam 6", "cam 7"]
commandlist = ["shut left", "shut right", "open left", "open right", "light left", "light right", "cam open",
               "cam close", "honk", "check scottgames.com", "wait"]
passivecommandlist = ["time", "power", "commandlist", "camlist", "debug"]  # Sets lists of valid commands
time = float(0)  # This is set as a float so that it can vary between each time, but it is later printed as a integer
power = int(100)  # Power, however, is an integer, as it does not go into decimals.
doors = [True, True]  # True = door open, first one is left
camera = [False, "0"]  # True = camera open, second variable is camera
lights = [False, False]  # First is left, second is right
night = int(0)  # night 0 op nerf pls
dead = False
debugused = False
animatronics = {"Freddy": ["0", int(7)], "Bonnie": ["0", int(5)], "Chica": ["0", int(7)],
                "Foxy": ["2", int(18)]}  # Sets the animatronic variables inside lists inside a dictionary. Recursion.

### - Debug Setup - ###

debug = str("Night " + str(night) + "\n")  # This is so useful it deserves its own subsection.


### - Door Setup - ###

def Door(Open, Left):  # Left = list value, Open 0 = Open
    if Open == 0:
        if doors[Left] == False:
            doors[Left] = True  # Opens the door
            print("You open the door.")
        else:
            print("You go to open the door, but it is already opened. You waste valuable time.")
    else:
        if doors[Left] == True:
            doors[Left] = False  # Closes the door
            print("You shut the door.")
        else:
            print("You go to shut the door, but it is already closed. You waste valuable time.")


##### - = - ENGAGE THE GAME - = - #####

print(
    "You are a security guard working in a pizzeria. It is midnight. For a command list, type 'commandlist' without the quotations.")

while time < 6:

    ##### - Player Command - #####

    # - Command List - #
    # shut left/right
    # open left/right
    # light left/right
    # cam open/close
    # switch camnumber
    # time
    # power
    # honk
    # wait

    command = 0
    debug = debug + ("\n")
    while command not in commandlist:  # This keeps the program looping. I do not need to refer to the camlist yet.
        command = input("Enter command: ")
        if command not in commandlist and command not in camlist:
            if command not in passivecommandlist:
                print("Invalid command.")
                debug = debug + str("Player requests " + command + ". Invalid command.\n")
            else:
                if command == passivecommandlist[0]:
                    print("The current time is " + str(int(time)) + " am.")
                elif command == passivecommandlist[1]:
                    print("Power levels: " + str(power) + "%")
                elif command == passivecommandlist[2]:
                    print("""shut left/shut right -> shuts the respective door
open left/open right -> opens the respective door
light left/light right -> flashes the respective light on and off
cam open/cam close -> opens/closes the camera system
cam (camnumber) -> switches to the camera location provided. For a camera list, type "camlist"
time -> displays the time. Doesn't use up an action.
power -> displays the power. Doesn't use up an action.
commandlist -> displays this message. Doesn't use up an action.
camlist -> displays a list of cameras. Doesn't use up an action.
wait -> does nothing. Useful if you're waiting for something, surprisingly. Also allows you to focus on the noises in the Kitchen.""")
                elif command == passivecommandlist[3]:
                    print("""1A = Show Stage. Connected to location 1B and 5.
1B = Dining Area. Connected to location 1A, 2A, 4A, 5, 6 and 7.
1C = Pirate Cove. Connected to location 2A.
2A = West Hall. Connected to location 1B, 2B, 3 and 5.
2B = West Hall Corner. Connected to location 2A, 3, and the Office.
3 = Supply Closet. Connected to location 2A and 2B.
4A = East Hall. Connected to location 1B, 4B and 6.
4B = East Hall Corner. Connected to location 4B, 6 and the Office.
5 = Backstage. Connected to location 1B and 2A.
6 = Kitchen. Only audio displays from here. 1B, 4A and 4B.
7 = Bathroom. Connected to location 1B and 6.""")
                else:
                    print(debug)
                    debug = debug + str("Player requests " + command + ". Passive.\n")
                    debugused = True
        else:
            debug = debug + str("Player requests " + command + ".\n")
            break

    ##### - Command processing - #####

    if command in commandlist:
        if command == commandlist[0]:
            if camera[0] == False:
                if animatronics["Freddy"][1] == 13 or animatronics["Bonnie"][1] == 13:
                    print("You press the left door button. It merely clicks.")
                else:
                    Door(1, 0)  # Open left
            else:
                print("You can't, for the camera system is still up. You waste valuable time.")
        elif command == commandlist[1]:
            if camera[0] == False:
                if animatronics["Freddy"][1] == 13 or animatronics["Chica"][1] == 13:
                    print("You press the right door button. It merely clicks.")
                else:
                    Door(1, 1)  # Open right
            else:
                print("You can't, for the camera system is still up. You waste valuable time.")
        elif command == commandlist[2]:
            if camera[0] == False:
                if animatronics["Freddy"][1] == 13 or animatronics["Bonnie"][1] == 13:
                    print("You press the left door button. It merely clicks.")
                else:
                    Door(0, 0)  # Shut left
            else:
                print("You can't, for the camera system is still up. You waste valuable time.")
        elif command == commandlist[3]:
            if camera[0] == False:
                if animatronics["Freddy"][1] == 13 or animatronics["Chica"][1] == 13:
                    print("You press the right door button. It merely clicks.")
                else:
                    Door(0, 1)  # Shut right
            else:
                print("You can't, for the camera system is still up. You waste valuable time.")
        elif command == commandlist[4]:
            if camera[0] == False:
                if animatronics["Freddy"][1] == 13 or animatronics["Bonnie"][1] == 13:
                    print("You press the left light button. It merely clicks.")
                else:
                    print("You turn the left light on.")
                    power = power - 1
            else:
                print("You can't, for the camera system is still up. You waste valuable time.")
        elif command == commandlist[5]:
            if camera[0] == False:
                if animatronics["Freddy"][1] == 13 or animatronics["Chica"][1] == 13:
                    print("You press the right light button. It merely clicks.")
                else:
                    print("You turn the right light on.")
                    power = power - 1
            else:
                print("You can't, for the camera system is still up. You waste valuable time.")
        elif command == commandlist[6]:
            if camera[0] == False:
                camera[0] = True  # True = Camera system up
                print("You flip the camera system up.")
                debug = debug + str("Successful.\n")
            else:
                print("The camera system is already open. You waste valuable time.")
                debug = debug + str("Unsuccessful.\n")
        elif command == commandlist[7]:
            if camera[0] == True:
                camera[0] = False
                print("You close the camera system.")
                debug = debug + str("Successful.\n")
            else:
                print("The camera system is already closed. You waste valuable time.")
                debug = debug + str("Unsuccessful.\n")
        elif command == commandlist[8]:
            if camera[0] == False:
                print("You look at the poster of the Freddy Band, and push Freddy's nose. It makes a satisfying sound.")
                debug = debug + str("Successful.\n")
            else:
                print(
                    "You obtain an undieing urge to push the poster of the Freddy Band, but your camera system is in the way.")
                debug = debug + str("Unsuccessful.\n")
        elif command == commandlist[9]:
            print(
                "You check scottgames.com on your camera system. It's still showing that nightmare image. You wonder whether you'll get fired for slacking off.")
        else:
            print("You wait about.")
    else:
        if command in camlist:
            if camera[0] == True:
                if command == camlist[0]:
                    if camera[1] != "0":
                        camera[1] = "0"
                        print("You switch to CAM 1A.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 1A. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[1]:
                    if camera[1] != "1":
                        camera[1] = "1"
                        print("You switch to CAM 1B.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 1B. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[2]:
                    if camera[1] != "2":
                        camera[1] = "2"
                        print("You switch to CAM 1C.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 1C. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[3]:
                    if camera[1] != "3":
                        camera[1] = "3"
                        print("You switch to CAM 2A.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 2A. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[4]:
                    if camera[1] != "4":
                        camera[1] = "4"
                        print("You switch to CAM 2B.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 2B. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[5]:
                    if camera[1] != "5":
                        camera[1] = "5"
                        print("You switch to CAM 3.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 3. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[6]:
                    if camera[1] != "6":
                        camera[1] = "6"
                        print("You switch to CAM 4A.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 4A. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[7]:
                    if camera[1] != "7":
                        camera[1] = "7"
                        print("You switch to CAM 4B.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 4B. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[8]:
                    if camera[1] != "8":
                        camera[1] = "8"
                        print("You switch to CAM 5.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 5. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                elif command == camlist[9]:
                    if camera[1] != "9":
                        camera[1] = "9"
                        print("You switch to CAM 6.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 6. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
                else:
                    if camera[1] != "10":
                        camera[1] = "10"
                        print("You switch to CAM 7.")
                        debug = debug + str("Successful.\n")
                    else:
                        print("You are already viewing CAM 7. You waste valuable time.")
                        debug = debug + str("Unsuccessful - already viewing.\n")
            else:
                print("You go to switch cameras, but the camera system is not open yet. You waste valuable time.")
                debug = debug + str("Unsuccessful - camera system not open.\n")

    ##### - Animatronic reaction - #####

    # 0 = 1A = Show Stage
    # 1 = 1B = Dining Area
    # 2 = 1C = Pirate Cove
    # 3 = 2A = West Hall
    # 4 = 2B = West Hall Corner
    # 5 = 3 = Supply Closet
    # 6 = 4A = East Hall
    # 7 = 4B = East Hall Corner
    # 8 = 5 = Backstage
    # 9 = 6 = Kitchen (audio only)
    # 10 = 7 = Bathroom
    # 11 = ? = Left Door
    # 12 = ?  Right Door
    # 13 = ? = Office

    # -- Animatronic Movement AI -- #

    # - Freddy - #
    # 1A -> 1B, (power) Office
    # 1B -> 7, (power) Office
    # 7 -> 6, (power) Office
    # 6 -> 4A, (power) Office
    # 4A -> 4B, (power) Office
    # 4B -> (right door) Office, (power) Office

    # - Bonnie - #
    # 1A -> 1B, 5
    # 1B -> 5, 2A
    # 5 -> 1B, 2A
    # 2A -> 2B, 3, 1B
    # 2B -> 2A, 3, Left Door
    # 3 -> 2A, 2B
    # Left Door -> 2B, (left door) Office

    # - Chica - #
    # 1A -> 1B
    # 1B -> 4A, 6, 7
    # 7 -> 1B
    # 6 -> 1B, 4A
    # 4A -> 1B, 6, 4B
    # 4B -> 4A, 6, Right Door
    # Right Door -> 4B, (right door) Office

    # - Foxy - #
    # 1C -> 2A
    # 2A -> (left door) Office, 1C

    # - Golden - #
    # 2B -> Office
    # Office -> Disabled

    # print(animatronics["Freddy"][1])
    # - remember this pls

    ### - Bonnie (he has a stupid face) - ###

    if animatronics["Bonnie"][1] != 0:  # If this is true, Bonnie's timer is over
        animatronics["Bonnie"][1] = (animatronics["Bonnie"][1]) - 1
        debug = debug + str("Bonnie counter changes to " + str(animatronics["Bonnie"][1]) + ".\n")
    else:
        if animatronics["Bonnie"][0] == "0":  # 1A -> 1B, 5
            if randint(1, 3) == 3:
                animatronics["Bonnie"][0] = "8"
            else:
                animatronics["Bonnie"][0] = "1"
            debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
        elif animatronics["Bonnie"][0] == "1":  # 1B -> 5, 2A
            if randint(1, 3) == 3:
                animatronics["Bonnie"][0] = "8"
            else:
                animatronics["Bonnie"][0] = "3"
            debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
        elif animatronics["Bonnie"][0] == "3":  # 2A -> 2B, 3, 1B
            if randint(1, 3) == 3:
                animatronics["Bonnie"][0] = "5"
            elif randint(1, 3) == 1:
                animatronics["Bonnie"][0] = "1"
            else:
                animatronics["Bonnie"][0] = "4"
            debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
        elif animatronics["Bonnie"][0] == "4":  # 2B -> 2A, 3, Left Door
            if randint(1, 3) == 3:
                animatronics["Bonnie"][0] = "3"
            elif randint(1, 3) == 3:
                animatronics["Bonnie"][0] = "5"
            else:
                animatronics["Bonnie"][0] = "11"
            debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
        elif animatronics["Bonnie"][0] == "5":  # 3 -> 2A, 2B
            if randint(1, 2) == 1:
                animatronics["Bonnie"][0] = "4"
            else:
                animatronics["Bonnie"][0] = "3"
            debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
        elif animatronics["Bonnie"][0] == "8":  # 5 -> 1B, 2A
            if randint(1, 2) == 2:
                animatronics["Bonnie"][0] = "3"
            else:
                animatronics["Bonnie"][0] = "1"
            debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
        elif animatronics["Bonnie"][
            0] == "11":  # If the door is open, Bonnie enters the office. Otherwise, he goes back the West Hall Corner.
            if doors[0] == True:
                if lights[0] != True:
                    animatronics["Bonnie"][0] = "13"
                    debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
            else:
                animatronics["Bonnie"][0] = "4"
                debug = debug + str("Bonnie moves to " + str(animatronics["Bonnie"][0]) + ".\n")
        else:
            print("Bonnie suddenly lunged towards you, grabbing your body and dragging it backstage.")
            dead = True
            killer = "Bonnie"
            debug = debug + str("Player killed by Bonnie.\n")
            break
        if animatronics["Bonnie"][0] == "11":
            animatronics["Bonnie"][1] = int(4)
        else:
            animatronics["Bonnie"][1] = int(3)
        debug = debug + str("Bonnie counter changes to " + str(animatronics["Bonnie"][1]) + ".\n")

    ### - Chica (she really loves to eat) - ###

    if animatronics["Chica"][1] != 0:  # If this is true, Chica's timer is over
        animatronics["Chica"][1] = (animatronics["Chica"][1]) - 1
        debug = debug + str("Chica counter changes to " + str(animatronics["Chica"][1]) + ".\n")
    else:
        if animatronics["Chica"][0] == "0":  # 1A -> 1B
            animatronics["Chica"][0] = "1"
            debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
        elif animatronics["Chica"][0] == "1":  # 1B -> 6, 7, 4A
            if randint(1, 4) == 4:
                animatronics["Chica"][0] = "9"
            elif randint(1, 3) == 3:
                animatronics["Chica"][0] = "10"
            else:
                animatronics["Chica"][0] = "6"
            debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
        elif animatronics["Chica"][0] == "6":  # 4A -> 1B, 6, 4B
            if randint(1, 6) == 6:
                animatronics["Chica"][0] = "1"
            elif randint(1, 2) == 1:
                animatronics["Chica"][0] = "9"
            else:
                animatronics["Chica"][0] = "7"
            debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
        elif animatronics["Chica"][0] == "7":  # 4B -> 4A, 6, Right Door
            if randint(1, 3) == 3:
                animatronics["Chica"][0] = "6"
            elif randint(1, 3) == 3:
                animatronics["Chica"][0] = "9"
            else:
                animatronics["Chica"][0] = "12"
            debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
        elif animatronics["Chica"][0] == "9":  # 6 -> 1B, 4A
            if randint(1, 5) == 1:
                animatronics["Chica"][0] = "1"
            else:
                animatronics["Chica"][0] = "6"
            debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
        elif animatronics["Chica"][0] == "10":  # 7 -> 1B
            animatronics["Chica"][0] = "1"
            debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
        elif animatronics["Chica"][
            0] == "12":  # If the door is open, Chica enters the office. Otherwise, she goes back the East Hall Corner.
            if doors[1] == True:
                if lights[1] != True:
                    animatronics["Chica"][0] = "13"
                    debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
            else:
                animatronics["Chica"][0] = "6"
                debug = debug + str("Chica moves to " + str(animatronics["Chica"][0]) + ".\n")
        else:
            print("Suddenly, Chica appeared in front of you, screaming.")
            dead = True
            killer = "Chica"
            debug = debug + str("Player killed by Chica.\n")
            break
        if animatronics["Chica"][0] == "11":
            animatronics["Chica"][1] = int(6)
            debug = debug + str("Chica counter changes to " + str(animatronics["Chica"][0]) + ".\n")
        else:
            animatronics["Chica"][1] = int(5)
            debug = debug + str("Chica counter changes to " + str(animatronics["Chica"][0]) + ".\n")

    ### - Freddy (secretly a paedophile) - ###

    if power <= 0:  # If the power is out, Freddy is instantly teleported to the office.
        animatronics["Freddy"][0] = "13"

    if animatronics["Freddy"][1] != 0:  # If this is true, Freddy's timer is over
        if camera[1] != animatronics["Freddy"][0] or camera[0] == False:
            animatronics["Freddy"][1] = (animatronics["Freddy"][1]) - 1
            debug = debug + ("Freddy counter changes to " + str(animatronics["Freddy"][1]) + ".\n")
    else:
        if animatronics["Freddy"][0] == "0":  # 1A -> 1B
            animatronics["Freddy"][0] = "1"
            debug = debug + str("Freddy moves to " + str(animatronics["Freddy"][0]) + ".\n")
        elif animatronics["Freddy"][0] == "1":  # 1B -> 7
            animatronics["Freddy"][0] = "9"
            debug = debug + str("Freddy moves to " + str(animatronics["Freddy"][0]) + ".\n")
        elif animatronics["Freddy"][0] == "9":  # 7 -> 6
            animatronics["Freddy"][0] = "8"
            debug = debug + str("Freddy moves to " + str(animatronics["Freddy"][0]) + ".\n")
        elif animatronics["Freddy"][0] == "8":  # 6 -> 4A
            animatronics["Freddy"][0] = "6"
            debug = debug + str("Freddy moves to " + str(animatronics["Freddy"][0]) + ".\n")
        elif animatronics["Freddy"][0] == "6":  # 4A -> 4B
            animatronics["Freddy"][0] = "7"
            debug = debug + str("Freddy moves to " + str(animatronics["Freddy"][0]) + ".\n")
        elif animatronics["Freddy"][0] == "7":  # 4B -> Office or 4A
            if doors[1] == True:
                animatronics["Freddy"][0] = "13"
                debug = debug + str("Freddy moves to " + str(animatronics["Freddy"][0]) + ".\n")
            else:
                animatronics["Freddy"][0] = "6"
                debug = debug + str("Freddy moves to " + str(animatronics["Freddy"][0]) + ".\n")
        else:
            print("Suddenly, your body is jerked backwards, and you see Freddy's head.")
            dead = True
            killer = "Freddy"
            debug = debug + str("Player killed by Freddy.\n")
            break
        animatronics["Freddy"][1] = int(8)
        debug = debug + str("Freddy counter changes to " + str(animatronics["Freddy"][1]) + ".\n")

    ### - Foxy (he only accepts liscenced merchendise) - ###

    if animatronics["Foxy"][0] == "2":
        if camera[1] == "2":
            if animatronics["Foxy"][1] < 18 and camera[0] == True:
                animatronics["Foxy"][1] = (animatronics["Foxy"][1]) + 1
            else:
                animatronics["Foxy"][1] = (animatronics["Foxy"][1]) - 1
            debug = debug + ("Foxy counter changes to " + str(animatronics["Foxy"][1]) + ".\n")
        else:
            animatronics["Foxy"][1] = (animatronics["Foxy"][1]) - 1
            debug = debug + ("Foxy counter changes to " + str(animatronics["Foxy"][1]) + ".\n")
            if animatronics["Foxy"][1] == 0:
                animatronics["Foxy"][0] = "3"
                debug = debug + str("Foxy moves to " + str(animatronics["Freddy"][0]) + ".\n")
                animatronics["Foxy"][1] = 4
                debug = debug + ("Foxy counter changes to " + str(animatronics["Foxy"][1]) + ".\n")
    else:
        if animatronics["Foxy"][1] == 0:
            if doors[0] == False:
                animatronics["Foxy"][0] = "2"
                debug = debug + str("Foxy moves to " + str(animatronics["Foxy"][0]) + ".\n")
                power = power - 5
                print("You hear a thud against the left door.")
                debug = debug + str("Foxy hit left door, power - 5.\n")
                animatronics["Foxy"][1] = int(18)
                debug = debug + ("Foxy counter changes to " + str(animatronics["Foxy"][1]) + ".\n")
            else:
                print("Suddenly, Foxy charged through the left doorway, and straight towards you.")
                dead = True
                killer = "Foxy"
                debug = debug + str("Player killed by Foxy.\n")
                break
        else:
            animatronics["Foxy"][1] = (animatronics["Foxy"][1]) - 1
            debug = debug + ("Foxy counter changes to " + str(animatronics["Foxy"][1]) + ".\n")

    ##### - Other - #####

    # nothing will probably end up going here#

    ##### - Feedback - #####

    if camera[0] == False:
        if command == commandlist[4]:
            if animatronics["Bonnie"][0] == "11":
                if doors[0] == True:
                    print("Bonnie stares at you through the doorway.")
                else:
                    print("You can see a shadow.")
            else:
                print("Nothing can be seen.")
        elif command == commandlist[5]:
            if animatronics["Chica"][0] == "12":
                if doors[1] == True:
                    print("Chica stares at you through the doorway.")
                else:
                    print("You can see a shadow.")
            else:
                print("Nothing can be seen.")
    else:
        if camera[1] == "0":
            if animatronics["Freddy"][0] == "0" and animatronics["Bonnie"][0] == "0" and animatronics["Chica"][
                0] == "0":
                print("Freddy, Chica and Bonnie stand on the stage, lifelessly. All three stare at the camera.")
            elif animatronics["Freddy"][0] == "0" and animatronics["Chica"][0] == "0":
                print("Freddy and Chica stand on the stage. Chica twitches slightly.")
            elif animatronics["Freddy"][0] == "0" and animatronics["Bonnie"][0] == "0":
                print("Freddy and Bonnie stand on the stage. Bonnie is juttering slightly.")
            elif animatronics["Chica"][0] == "0" and animatronics["Bonnie"][0] == "0":
                print("Chica and Bonnie stand on stage, both twitching.")
            elif animatronics["Freddy"][0] == "0":
                print("Freddy is standing on stage.")
            elif animatronics["Chica"][0] == "0":
                print("Chica is standing on stage.")
            elif animatronics["Bonnie"][0] == "0":
                print("Bonnie is standing on stage.")
            else:
                print("The show stage is empty.")
        elif camera[1] == "1":
            if animatronics["Freddy"][0] == "1" and animatronics["Bonnie"][0] == "1" and animatronics["Chica"][
                0] == "1":
                print("Freddy, Chica and Bonnie all stand lifelessly, staring at the camera.")
            elif animatronics["Freddy"][0] == "1" and animatronics["Chica"][0] == "1":
                print("Freddy and Chica stand in the dining area. There are tables knocked over near Chica.")
            elif animatronics["Freddy"][0] == "1" and animatronics["Bonnie"][0] == "1":
                print(
                    "Freddy and Bonnie are standing in the dining area. Freddy's eyes create a glare on the camera, limiting your view.")
            elif animatronics["Chica"][0] == "1" and animatronics["Bonnie"][0] == "1":
                print("Chica and Bonnie stand in the dining area, motionless.")
            elif animatronics["Freddy"][0] == "1":
                print("Freddy's eyes pierce out of the darkness.")
            elif animatronics["Chica"][0] == "1":
                print("Chica is in the dining area.")
            elif animatronics["Bonnie"][0] == "1":
                print("Bonnie is in the dining area.")
            else:
                print("The dining area is empty.")
        elif camera[1] == "2":
            if animatronics["Foxy"][0] != "2":
                print("The curtains are open. The pirate cove is empty.")
            else:
                if animatronics["Foxy"][1] > 12:
                    print("The curtains are closed.")
                elif animatronics["Foxy"][1] > 6:
                    print("Foxy's head is staring through the curtains.")
                else:
                    print("Foxy's body is mostly out of the curtains, attempting to run out.")
        elif camera[1] == "3":
            if animatronics["Bonnie"][0] == "3" and animatronics["Foxy"][0] == "3":
                print("Foxy is charging through the hallway. Bonnie stands by, lifelessly.")
            elif animatronics["Bonnie"][0] == "3":
                print("Bonnie is standing in the dark corners of the hallway.")
            elif animatronics["Foxy"][0] == "3":
                print("Foxy is charging through the hallway.")
            else:
                print("The hallway is empty.")
        elif camera[1] == "4":
            if animatronics["Bonnie"][0] == "4":
                print("Bonnie stares into the camera, obscuring your vision.")
            else:
                print("The hallway corner is empty.")
        elif camera[1] == "5":
            if animatronics["Bonnie"][0] == "5":
                print("Bonnie is standing underneath the light, looking directly forward.")
            else:
                print("The supply closet is empty, spare the brooms lieing on the wall.")
        elif camera[1] == "6":
            if animatronics["Chica"][0] == "6" and animatronics["Freddy"][0] == "6":
                print("Chica is in the middle of the hallway. Behind her, you can make out Freddy's silohette.")
            elif animatronics["Chica"][0] == "6":
                print("Chica is standing near the back of the hallway.")
            elif animatronics["Freddy"][0] == "6":
                print("Freddy is in the shadows of the hallway, staring at the camera.")
            else:
                print("The hallway is empty.")
        elif camera[1] == "7":
            if animatronics["Freddy"][0] == "7":
                print(
                    "Freddy's head completely obscures the camera, his eyes causing a terrible glare on the camera. You cannot check if there in an animatronic behind him.")
            elif animatronics["Chica"][0] == "7":
                print("Chica is standing against the corners of the wall, looking up at the camera.")
            else:
                print("The hallway is empty.")
        elif camera[1] == "8":
            if animatronics["Bonnie"][0] == "5":
                if command == "cam open":
                    print("Bonnie is staring directly at the camera, his souless eyes piercing your view.")
                else:
                    print("Bonnie is standing in the room.")
            else:
                print("The backstage area is empty, spare an endoskeleton on the table.")
        elif camera[1] == "9":
            if command == "wait":
                if animatronics["Chica"][0] == "9" and animatronics["Freddy"][0] == "9":
                    print(
                        "The camera is disabled. Focusing on the noises, you can hear pans and pots being scraped about, muffling out a fainter music box.")
                elif animatronics["Chica"][0] == "9":
                    print(
                        "The camera is disabled. Focusing on the noises, you can hear pans and pots being scraped about.")
                elif animatronics["Freddy"][0] == "9":
                    print("The camera is disabled. Focusing on the noises, you can hear a music box.")
                else:
                    print("The camera is disabled. You can not hear any noises.")
            else:
                if animatronics["Chica"][0] == "9" or animatronics["Freddy"][0] == "9":
                    print("The camera is disabled. You can hear noises.")
                else:
                    print("The camera is disabled. You can not hear any noises.")
        else:
            if animatronics["Chica"][0] == "10" and animatronics["Freddy"][0] == "10":
                print(
                    "Chica is staring directly at the camera. In the darkness, you can see Freddy peering out of the ladies' bathroom.")
            elif animatronics["Chica"][0] == "10":
                print("Chica is standing near the entrance to the bathrooms.")
            elif animatronics["Freddy"][0] == "10":
                print("Freddy is peering out of the ladies' bathroom.")
            else:
                print("The bathroom is empty.")

    ##### - Power Calcs - #####

    if camera[0] == True:
        power = power - 1

    if doors[0] == False:
        power = power - 2
    if doors[1] == False:
        poewr = power - 2

    if power <= 0:
        print(
            "Suddenly, the power cuts off. You see white eyes piercing at you from the west hallway. That is the last thing you see.")
        dead = True
        killer = "Freddy"
        break
    ##### - Time - #####

    time = time + 0.1

    ##### - Loop here - #####

#### - Postgame - #####

if dead == True:
    print("You were killed. Game over.")
    input()
#    if debugused == False:
#        file = open("Leaderboards.txt", "a")
#        temp = input("Enter name: ")
#        file.write("\n" + temp + " was killed by " + killer + " at " + str(int(time)) + " am, with " + str(power) + "% power.")
#        file.close()
else:
    print("The clock turns to 6am, and you hear church bells ringing. You made it!\n")
    input()
#    if debugused == False:
#        file = open("Leaderboards.txt", "a")
#        temp = input("Enter name: ")
#        file.write("\n" + temp + " survived to 6 am, with " + str(power) + "% power.")
#        file.close()

# This is commented out because it existed purely to make this project count as homework.
