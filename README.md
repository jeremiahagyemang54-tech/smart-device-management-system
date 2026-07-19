# smart-device-management-system
class SmartDevice:
    def init(self,name,device_id,power_status):
        self.name = name
        self.__device_id = device_id
        self.__power_status = power_status

    @property
    def device_id(self):
        return self.__device_id

    @device_id.setter
    def device_id(self, actual_id):
        if actual_id == "":
            print("NO!!!: Device ID cannot be empty.")

        else:
            self.__device_id = actual_id

    @property
    def power_status(self):
        return self.__power_status

    @power_status.setter
    def power_status(self, status):
        self.__power_status = status

    def turn_on(self):
        self.__power_status = True
        print(f"Turning on {self.name} \n{self.name} is now on")

    def turn_off(self):
        self.__power_status = False
        print(f"Turning off {self.name} \n{self.name} is now off")

    def display_info(self):
        print(f"Name : {self.name} \nDevice ID : {self.device_id}")
        if self.power_status:
            print(f"Power Status : ON")
        else:
            print(f"Power Status : OFF ")

class TemperatureSensor(SmartDevice):
    def init(self,name,device_id,power_status,temperature):
        super().init(name,device_id,power_status)
        self.temperature = temperature

    def read_temperature(self):
        if self.power_status:
            print(f"Temperature reading {self.name} is {self.temperature}°C.")###
        else:
            print(f"{self.name} is off ")

class SecurityCamera(SmartDevice):
    def init(self,name,device_id,power_status,recording_status):
        super().init(name, device_id, power_status)
        self.recording_status = recording_status

    def display_info(self):
        super().display_info()
        print("Recording_status : ","ON" if {self.recording_status} else "OFF")

    def start_recording(self):
        if self.power_status:
            self.recording_status = True
            print(f"Recording is now active on {self.name}")
        else:
            print(f"Action unsuccessful. {self.name} please turn it off first")

    def stop_recording(self):
        if self.power_status:
            self.recording_status = False
            print(f"Recording is no longer active on {self.name}")
        else:
            print(f"The system is shut down and inactive")



class SmartLight(SmartDevice):
    def init(self,name,device_id,power_status,brightness):
        super().init(name, device_id, power_status)
        self.brightness = brightness

    def increase_brightness(self,amount):
        if 0< amount <100:
            print(f"{self.name}'s brightness level is increasing")
            if self.power_status:
                self.brightness = self.brightness + amount
                if self.brightness > 100:
                    self.brightness = 100
                    print(f"Brightness limit reached at {self.brightness}%")###
                else:
                    print(f"Brightness set to: {self.brightness}%")###
            else:
                print(f"Turn on {self.name}")
        else:
            print(f"Error: Type a number between 1 and 99 only")

    def decrease_brightness(self,amount):
        if 0< amount <100:
            print(f"Dimming the light for {self.name}...")###
            if self.power_status:
                self.brightness = self.brightness - amount
                if self.brightness < 0:
                    self.brightness = 0
                    print("Brightness cannot go lower than 0%")###
                else:
                    print(f"Brightness reduced to: {self.brightness}%")###
            else:
                print(f"Turn on {self.name}")
        else:
            print(f"Enter a number between 1 and 99")



my_sensor = TemperatureSensor("Kitchen Sensor", 4444, True, 19)
my_light = SmartLight("Hall Light", 5555, True, 50)
my_cam = SecurityCamera("Front Gate Camera", 6666, True, True)

print("<<<< SMART HOME CONTROL PANEL >>>>")###

is_running = True
while is_running:
    print("** OPTIONS **")###
    print("1. Display Device Information")
    print("2. Turn Device On")
    print("3. Turn Device Off")
    print("4. Read Temperature")
    print("5. Adjust Brightness")
    print("6. Start Recording")
    print("7. Exit")

    try:
        option = int(input("Type an option number (1-7): "))
    except ValueError:
        print("Input error!")###
        print("enter a number between 1 and 7")
        continue


    if option == 1:
        my_sensor.display_info()
        my_light.display_info()
        my_cam.display_info()

    elif option == 2:
        print("Which device would you like to turn on?")
        print("1. Thermometer 2. Light 3. Camera")
        device_option = int(input("Choose an option(1-3): "))

        if device_option == 1:
            my_sensor.turn_on()
        elif device_option == 2:
            my_light.turn_on()
        elif device_option == 3:
            my_cam.turn_on()
        else:
            print("Invalid option")

    elif option == 3:
        print("Which device would you like to turn off?")
        print("1. Thermostat 2. Light 3. Camera")
        device_option = int(input("Choose an option(1-3): "))

        if device_option == 1:
            my_sensor.turn_off()
        elif device_option == 2:
            my_light.turn_off()
        elif device_option == 3:
            my_cam.turn_off()
        else:
            print("Selection not part")

    elif option == 4:
        my_sensor.read_temperature()

    elif option == 5:
        print("Select brightness adjustment direction:")
        print("1. Increase Brightness 2. Decrease Brightness")

        brightness_option = int(input("Enter 1 for increae or 2 for decrease: "))
        amount = int(input("Enter brightness change amount: "))###
        if brightness_option == 1:
            my_light.increase_brightness(amount)
        elif brightness_option == 2:
            my_light.decrease_brightness(amount)
        else:
            print("Invalid option")

    elif option == 6:
        rec_option = str(input("Activate recording? (Yes / No): "))
        if rec_option.capitalize() == "Yes":
            my_cam.start_recording()

    elif option == 7:
        is_running = False
        print("Shutting down Panel...")

    else:
        print("Invalid Selection!!")
        print("Please pick from 1 to 7")



        while is_running:
    print("** OPTIONS **")###
    print("1. Display Device Information")
    print("2. Turn Device On")
    print("3. Turn Device Off")
    print("4. Read Temperature")
    print("5. Adjust Brightness")
    print("6. Start Recording")
    print("7. Exit")

    try:
        option = int(input("Type an option number (1-7): "))
    except ValueError:
        print("Input error!")###
        print("enter a number between 1 and 7")
        continue


    if option == 1:
        my_sensor.display_info()
        my_light.display_info()
        my_cam.display_info()

    elif option == 2:
        print("Which device would you like to turn on?")
        print("1. Thermometer 2. Light 3. Camera")
        device_option = int(input("Choose an option(1-3): "))

        if device_option == 1:
            my_sensor.turn_on()
        elif device_option == 2:
            my_light.turn_on()
        elif device_option == 3:
            my_cam.turn_on()
        else:
            print("Invalid option")

    elif option == 3:
        print("Which device would you like to turn off?")
        print("1. Thermostat 2. Light 3. Camera")
        device_option = int(input("Choose an option(1-3): "))

        if device_option == 1:
            my_sensor.turn_off()
        elif device_option == 2:
            my_light.turn_off()
        elif device_option == 3:
            my_cam.turn_off()
        else:
            print("Selection not part")

    elif option == 4:
        my_sensor.read_temperature()

    elif option == 5:
        print("Select brightness adjustment direction:")
        print("1. Increase Brightness 2. Decrease Brightness")

        brightness_option = int(input("Enter 1 for increae or 2 for decrease: "))
        amount = int(input("Enter brightness change amount: "))###
        if brightness_option == 1:
            my_light.increase_brightness(amount)
        elif brightness_option == 2:
            my_light.decrease_brightness(amount)
        else:
            print("Invalid option")

    elif option == 6:
        rec_option = str(input("Activate recording? (Yes / No): "))
        if rec_option.capitalize() == "Yes":
            my_cam.start_recording()

    elif option == 7:
        is_running = False
        print("Shutting down Panel...")

    else:
        print("Invalid Selection!!")
        print("Please pick from 1 to 7")

       Introduction of project
This project is called “Smart Home Control panel” which is designed to control and monitoring of devices in a home

Summary of the task
This program is a Smart Home Control Panel built using Python Object-Oriented Programming (OOP).
Ensure you have Python 3 installed on your workstation.

 Clone the repository:
