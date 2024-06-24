A framework for a fully modular ULTRAKILL playing agent

(A rewrite of [this](https://youtu.be/16zgLzC1eDE))

Original concept/code/idea/literally everything by [8AAFFF](https://www.youtube.com/@8AAFFF)

Code (mostly) rewritten by [CTAG](https://www.youtube.com/@ctag07)

(if anyone wants to reformat this readme with better markdown then please do, I don't know how to do markdown)


WARNING:
    This bot currently uses raw mouse movement for turning, so it can cause a lot of flashing and stuttering within it's movement.
    This is because mouse and keyboard input are a lot easier to control precisely 


HOW TO RUN:


    Change anything you want in the config.py file, they work are as follows:


        SENSOR_MODULES:

            A list of the sensor modules to include for the bot
            Sensor modules are things that take in a screenshot of the game and output data for other modules to use
            This has to include every required sensor module for the strategy and all action modules


        ACTION_MODULES:

            A list of the action modules to include for the bot
            Action modules take in data from sensor modules and use the interface to control v1
            You shouldn't have to include any specific action modules because strategies shouldn't be reliant on specific modules
            Add and remove modules as you please, but if the strategy you use doesn't have a module implemented it won't be used


        STRATEGY:

            The strategy module that you want to use
            Strategy modules take in data from sensor modules and decide which action module should be run each iteration
            This can be any strategy module you want
        

        INTERFACE_DATA:

            A list of numbers important for the bot to be able to properly play, make sure to fill all these out with your own values beforehand!
            The bot uses some of these for things like deciding how much to turn, or how fast things should be run


    Then, run main.py and let it start up! (Make sure to alt tab into ultrakill before it's done starting up, otherwise it will take control of your keyboard early!)
    If you want to reload the bot at any time, press the home key
    If you want to stop the bot at any time, press the end key


MAKING MODULES:


    This framework is designed to be hyper-modular, with literally everything contained within a module that's plug-and-play at all times.


    SENSOR MODULES:

        Look at the base_sensor_module.py for an example of how a sensor module should be structured
        Create a new python file in the sensor modules folder, and create a class there that inherits from the base sensor module class
        Then implement the init and run methods for the sensor, making sure it outputs appropriate data for whatever kind of sensor it is


    ACTION MODULES:

        Look at the base_action_module.py for an example of how an action module should be structured
        Create a new python file in the action modules folder, and create a class there that inherits from the base action module class
        Then implement the init and run methods for the action module, with the init function calling the init method for it's parent class with the interface to set the interface variable
        Also make sure to update the required_sensors list with the list of sensors that the action module needs to run
        The data from these sensors will be input into the run function of your action module in the order that you list them in, so keep that in mind
        You can use the interface to do practically anything you need with v1
    

    STRATEGY MODULES:

        Look at the base_strategy.py for an example of how a strategy module should be structured
        Create a new python file in the strategies folder, and create a class there that inherits from the base strategy module class
        Then implement the init and run methods for the strategy module, with the init function calling the init method for it's parent class with the list of action module name and value pairs
        Also make sure to update the required_sensors list with the list of sensors that the strategy needs to run
        The data from these sensors will be input into the run function of your strategy in the order that you list them in, so keep that in mind
        Best practice is to make if statements to apply values for each module, so that if a module isn't present from the user it won't error, and it will make do with the enabled modules


I'm pretty sure the dude who originally made this should accept pr's and they're definitely appreciated
Can't wait to see how far this goes! :D