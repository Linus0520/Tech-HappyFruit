# HAPPY FRUIT TUTORIAL

## Preparation

>* PC with Webcam
>* Installed Processing(Go to Processing.org and download processing.)
>* Colorful items ( We used fruits in this project:  red apple, green apple, orange and lemon.)
>![items](/1.png)
>* Relative images(We designed happy fruit images.
>
>![apple](/apple.png) ![lemon](/lemon.png) ![pear](/pear.png) ![orange](/orange.png)

## Code explanation
###  Step 1: Install Library and Define objects

> Open Processing and download Video library in processing to connect to webcam. Define track color variables and fruit images.
```
import processing.video.*;
Capture video; 
PImage orange;
color trackColor; 
```
###  Step 2: Set up device and insert images
```
void setup() {
size(1280,720);
printArray(Capture.list());
video = new Capture(this,1280,720);
video.start();

trackColor = color(255,0,0);
smooth();

orange = loadImage("orange.png");
}
```
###  Step 3. Draw video pictures and track the colors
```
void draw() {
    background(0);

    if (video.available()) {
        video.read();
        }
    video.loadPixels();
    image(video,0,0); 
    
    float r2 = red(trackColor);
    float g2 = green(trackColor);
    float b2 = blue(trackColor);
    for(int x = 0; x < video.width; x++) {
        for(int y = 0; y < video.height; y++) {
 
        int currentLoc = x + y*video.width;
        color currentColor = video.pixels[currentLoc];
 
        float r1 = red(currentColor);
        float g1 = green(currentColor);
        float b1 = blue(currentColor);


        if(dist(r1,g1,b1,r2,g2,b2) < TOLERANCE) {
           somme_x += x;
           somme_y += y;
          compteur++;
        }

        else if(compteur > 0) { 
          XRc = somme_x / compteur;
          YRc = somme_y / compteur;
        }
     }
  }  
```
###  Step 4. Draw pictures at target
```
if(XRc != 0 || YRc != 0) { // Draw a circle at the first target
    image(orange,XRc-90.5,YRc-100, 181, 200);
  }
```
###  Step 5. Create mouse events
```
void mousePressed() {
  if (mousePressed && (mouseButton == RIGHT)) { 
      if(ii==0){  
      if (mouseY>480){mouseY=0; mouseX=0;}
      int loc = mouseX + mouseY*video.width;
      trackColor = video.pixels[loc];
      ii=1;  
  }else if(ii==1){  
      if (mouseY>480){mouseY=0;mouseX=0;}
      int loc2 = mouseX + mouseY*video.width;
      trackColor2 = video.pixels[loc2];
      ii=2;  
      } 
}
```
## Have fun!
> When webcam captures real fruit, click the fruit on screen, then the corresponding image will show up on screen. It means the webcam has already captured the color of the real fruit. The image will move on screen following the movement of real fruits.
