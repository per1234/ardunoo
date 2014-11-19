ArduNoo
=======

Noolite library for arduino. Works with modules like MT1132.

Warning! Not supported:
* Module selection (SE pin)
* LED controller commands

If you want to add them - pullrequest me ;) It is not so hard, but I am lazy...

Installation
------------

Unpack this into ~/sketchbooks/libraries (you must get catalog ~/sketchbooks/libraries/ardunoo).
Restart your Arduino IDE. That's all!

Usage: 
------

Let you connect MT1132 to your arduino like this:
````
+---------+               +---------+
| MT1132  +-(RX)-----(11)-+ Arduino |
|         +-(TX)-----(10)-+         |
|         |               |         |
````

Use sketch like this:

````
#include <ardunoo.h>

#define RXpin 10
#define TXpin 11

ArduNoo noo(RXpin,TXpin);

void setup(){
  Serial.begin(9600);
  noo.channel(5);     // Let's command 5-th channel
  // ...
}

void loop(){
  int r;
  r=Serial.read();
  if(r<='9' && r>='0'){ // change channel
    noo.channel(r-'0');
    return;
  }
  switch(r){
  case 'n': //on
    noo.on();
    break;
  case 'f': //off
    noo.off();
    break;
  case 'x': // toggle
    noo.onoff();
    break;
  case 'c': //print current channel
    Serial.print(noo.channel());
    break;
  case 'b': //bind
    noo.bind();
    break;
  case 'u': //unbind
    noo.unbind();
    break;
  case '+':
    noo.slow_on();
    break;
  case '-':
    noo.slow_off();
    break;
  case '!':
    noo.slow_onoff();
    break;

  case 'r': // record scene!
    noo.record_scene();
    break;
  case 'R': // run scene!
    noo.run_scene();
    break;

  case 's': // toggle 3-rd channel
    noo.onoff(3);
    break;
  }
}
````
