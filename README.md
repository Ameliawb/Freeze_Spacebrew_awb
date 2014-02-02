/*
 * FREEZE game via Spacebrew
 *
 *   Spacebrew library button example that has been modified by our group, Neva, Adrian,Karl and Edward and myself full credits on github
 using spacebrew for a class at ITP with Brett!
 * 
 */
import spacebrew.*;
float lastRun=0;
float waitTime=0;
boolean go;
long lastTime = 0;
String server="D--__-.itp.T---___.nyu.edu";//our itp sandbox server!!
String name="stop/go";
String description ="Client that sends and receives boolean messages.";

Spacebrew sb;

color color_on = color(255, 255, 50);
color color_off = color(255, 255, 255);
int currentColor = color_off;

void setup() {

  frameRate(240);
  size(500, 400);

  // instantiate the spacebrewConnection variable
  sb = new Spacebrew( this );

  // declare your publishers
  sb.addPublish( "stop/go", "boolean", true ); 


  // declare your subscribers
  sb.addSubscribe( "change_background", "boolean" );

  // connect to spacebre
  sb.connect(server, name, description );
}

void draw() {
  if (millis()>(lastRun+waitTime)) { 
    if (go == false) {
      go=true;
    }
    else {
      go=false;
    }
    GO();
    newWait();
    lastRun=millis();
  }
}

void GO() {
  // send message to spacebrew
  sb.send( "stop/go", go);
}


void newWait() {
  waitTime=random(5000)+1000;///naturally you should adjust this 5 seconds isn't enough running time this is just an example
}

void onBooleanMessage( String name, boolean go ) {
  println("got bool message " + name + " : " + go); 

 
}
