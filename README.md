# Obstacle Avoidance Solution

## Strategy
  
Braitenberg Vehicle 3b ("Explorer") uses inhibitory crossed connections between sensors and wheels.   
Left-side sensors inhibit the right wheel.   
Right-side sensors inhibit the left wheel.    
The robot continuously steers away from obstacles, no thresholds, no pivoting in place.    

Source: Braitenberg, V. (1984). Vehicles: Experiments in Synthetic Psychology. MIT Press.

## Old vs New — pseudocode comparison

```
OLD (gas particle):
  sum all 24 sensors into one averaged vector
  IF vector is small AND points roughly forward:
    both wheels = full speed
  ELSE:
    IF obstacle on left:  left wheel full, right wheel STOP
    ELSE:                 left wheel STOP, right wheel full
```

```
NEW (Braitenberg 3b):
  leftSpeed  = max_speed
  rightSpeed = max_speed
  FOR each sensor:
    IF sensor on left side (positive angle):  rightSpeed -= sensor.Value * max_speed
    IF sensor on right side (negative angle): leftSpeed  -= sensor.Value * max_speed
  clamp both to minimum 0
  set wheel speeds
```

## Build and test commands

### Clone this repo inside the /controllers directory of the examples repo replacing the existing folder

```bash
cd argos3-examples/controllers
rm -rf footbot_diffusion
git clone https://github.com/1337encrypted/footbot_diffusion-.git footbot_diffusion
```

### Build the source code

```bash
cd ../build
make
cd ..
```

### Run diffusion_10.argos

```bash
argos3 -c experiments/diffusion_10.argos
```
