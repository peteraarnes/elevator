
# NuSMV elevator thing
If you are reading this, you probably are vaguely familiar with NuSMV as a tool for model checking. Then you are also probably familiar with temporal logic (hurray!). The smv format which is the format that NuSMV can run is somewhat confusing markup-ish language.

This is some code for a previous school project. If you want confusing code, which doesn't work optimally, feel free to use this as inspiration.

There are four buttons which call the elevator to go up, and four to go down. There is only one first floor button which will request the elevator to go up. Likewise, the 5th floor only has one button which will request the elevator to go down. The floor 2, 3 and 5 will have buttons to request the elevator to go both up and down.

## MODULE Fire_alarm
Contains one boolean variable “fire”. As the name implies, it represents whether or not there is a fire. An instance of the Fire_alarm module will be Instantiated by MAIN. The Fire_Alarm module will be utilized in the Controller module. If fire = TRUE will determine if cmd_stop will become TRUE.
MODULE Elevator(cmd_up, cmd_down, cmd_none, cmd_stop)
The Elevator module has six different variables.

## Variables:
floor : 1..5 A set of integers {1, 2, 3, 4, 5}. Used in the ASSIGN section to check which floor the elevator is at, and where to move thereafter.
temperature : 0..6 A set of integers. 1 would represent 10°C. Reasons for not using a set of etc. 1..60 is to reduce possible states by a lot.
activateFan : boolean Represents when fan is active. Variable is TRUE when temperature >= 2.
2
over_weight_capacity : boolean Simple check to represent if the elevator has exceeded the weight limit.
door1 : boolean Used to define door_1_open
door2 : Boolean Used to define door_2_open
door_1_open / door_2_open represents when a given door (1 or 2) is allowed to be open.
ok_to_move_up / ok_to_move_down defines when the floor variable is allowed to be changed. cmd_up / cmd_down (defined in controller) refers to when the elevator is requested to move up or down. The elevator is allowed to move when no doors are open, the weight capacity is not exceeded and has been given a command by the Controller.

## cmd_stop could initiate a safety procedure if there is a fire. If the elevator is operating, it will ignore incoming requests, instead go directly to floor 1 and open the door to ensure the safety of passengers. It will be in service until there is no fire.
MODULE Controller (el1_floor, el1_door2, el1_door1, e2_floor, e2_door2, e2_door1, bf1up_pressed, bf2up_pressed, bf3up_pressed, bf4up_pressed, -- Floor button request up bf2down_pressed, bf3down_pressed, bf4down_pressed, bf5_pressed, fire_alarm)

## Parameter variables are derived from the other modules listed at earlier sections of the paper. Etc. el1 and e2, “e” refers to an elevator, integer 1 and 2 refers to which of the elevator the given variable is derived from.
The variables which are used in the button module are instantiated by the controller and assigned when the variable is TRUE. Etc.
reset_fb4Up := el1_floor = 5 | e2_floor = 5; Floor up-button for the 4th floor is TRUE, therefore allowed to be pressed again when elevator 1 or elevator 2 has reached 5th floor. Given an elevator iterate through each floor when moving upwards towards the floor which calls the elevator.
“reset_SOME_BUTTON”:= el1_floor = “N_FLOOR” | e2_floor = N_FLOOR” If FALSE, a sequence defined variables which assigns cmd_up, cmd_down, cmd_none are parsed by the elevator to module to move in the given direction.
