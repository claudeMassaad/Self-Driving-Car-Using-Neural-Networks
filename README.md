In this project I built a self driving car by equipping the car with a neural network system that helps the car make better decisions after some iterations and learning.

The car possesses 5 sensors that measure the distance between the car's edges and the obstacles in front of it. The different obastacles are other cars (in the DEMONSTRATION video those are the red cars) and the borders of the road. The car crashes if it hits the other cars or the road boarders.

Each car that I create has a different neural network configurations. The configurations of each car's neural network are randomized between edge values. I used many cars in the simulations (as you can see in the video, I varied the number of cars between 100 and 1000) and used a process similar to natural selection: the car that had the closest trajectory to the ideal trajectory (one where it would avoid all obstacles) had its neural network configurations saved in a JSON file by me manually (in the NEURAL NETWORK TRAINING video I was pressing on the save icon to save the configurations) on the local storage of my laptop. Then I would start the simulation again, but all the cars would have as their neural network configurations, the configurations of the best car that I had saved in the previous simulation. However; if they all have the same brain as the best car in the previous simulation, and considering that this best car did not avoid all obstacles in the previous simulation and crash, how would the cars in a new simulation behave differently and actually avoid all obstacles?
I created a function that mutates the configurations of a car relatively to best previous car: if the best previous car would go 40% to the left in a certain situation, the new car - that is supposed to behave exactly like the best car from the previous simulation - would rotate 70% or more to the left based on its new configurations. This way, by introducing a mutation in each new car's neural network configurations, we would see new cars behaving similarly to the best car in the previous simulation but not in the exact same way. Each car would change its trajectory a bit. 
I used a mutation factor that I could change manually based on the performances of the cars that I could see in front of me (I am the one deciding the natural selection variations of my cars, MOUAHAHA. DEUS EX MACHINA... Enough with the philosophical jokes).



Neural Network Functioning:

The neural network I designed for this project has 2 levels (or 3 layers). 

          x        x        x        x     <---------------- 4 nodes telling the car how to behave: first node on the left told the car to move forward,
                                                             second one told the car to move to the left, third one to right, and fourth one backwards
       
      
                                                        LEVEL 1
    
   
  
  x        x        x        x        x        x      <---------------- 6 nodes taking as inputs the readings from the sensor in the Layer1 and                                                                                   multiplying the values with randomized weights (randomized between certain values)
   
    
                                                        LEVEL 0
                                                        
       
       x        x        x        x        x      <---------------- 5 nodes (5 sensors on the car) receiving readings about the distance of car to obstacle


Bottom nodes are part of: Layer0; Middle nodes are part of: Layer1; Top nodes are part of: Layer2

Layer0 received the readings from the sensors of the car (represented as yellow rays in the video). The readings were about the difference distance between the edge of the car and the closest obstacle. Each node in Layer0 is connected to all nodes of Layer1, with each connection having different weights betweeen -1 and 1 that are randomized. When a node in Layer1 receives the distance as a reading, it applies to it a function that takes into consideration the randomized weight and a bias that it incorporates into a function and gives a certain result. Once this result is returned by the node, it is compared to this node's trigger level: for example lets say that a node has a trigger level of 0.4, any result under 0.4 would tell the node to send a certain message, any other result above 0.4 would send another message. The message that nodes on Layer1 can send is either a 1 or a 0, depending on if the result it got from applying the function was inferior or superior to its trigger level.
Each node of Layer1 emits either a "1" or "0" message to all nodes of Layer2 at all time. A message sent with "1" as recipient would mean that the node in Layer2 on the receiving end has to be activated. A message sent with "0" as recipient would mean that the node in Layer2 on the receiving end has to be deactivated. As you probably have guessed it, the nodes on Layer2 are the ones who give directions to the car: if the first node on the left receives a "1" then it moves the car forward. The second node on Layer2 is responsible to move the car to the left, thrid one to the right, and last one backwards.

To dod this project I inspired myself from Radu Istodor, from whom I took many functions as they were very complex to come up with. Thank you Radu!
