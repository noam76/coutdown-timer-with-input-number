# coutdown-timer-with-input-number
Add an input_number I choose timer_countdown name
Create a countdown timer that the user can adjust the time with an input_number.
  I choose water_heater for my timer name, you can choice yours.
Create a sensor to display the time.
  I choose timer_countdown_hour name, you can choice yours.
Convert the number to time format HH:MM.
Add new Script to start, stop, pause, cancel, finish
Add Lovelace card to use script and the elapsted time

setup:
1. add in configuration file your input_number
input number:
 timer_countdown:
   name: Countdown Timer
   icon: mdi:WatchVibrate
   min: 0
   max: 180
   mode: box
   step: 5

2. add in configuration file your timer name without duration
   timer:
     water_heater:

3. create a sensor template in sensor
sensor:
  - platform: template
    sensors:
      timer_countdown_hour:
       value_template: "{{ states('input_number.timer_countdown')|int|multiply(60)|timestamp_custom('%H:%M', false) }}"

4. add new script
script:
 start_timer_heater:
    alias: Start timer heater
    sequence:
      - service: timer.start
        entity_id: timer.water_heater
        data_template:
          duration:
            minutes: "{{ states('input_number.timer_countdown')|int }}"
  pause_timer_heater:
    alias: Pause timer heater
    sequence:
      - service: timer.pause
        entity_id: timer.water_heater
  cancel_timer_heater:
    alias: Cancel timer heater
    sequence:
      - service: timer.cancel
        entity_id: timer.water_heater
  finish_timer_heater:
    alias: Finish timer heater
    sequence:
      - service: timer.finish
        entity_id: timer.water_heater
        
5. finaly add entity to your new lovelace card
input_number.timer_countdown
script.start_timer_heater
script.pause_timer_heater
script.cancel_timer_heater
script.finish_timer_heater
timer.water_heater

enjoy
