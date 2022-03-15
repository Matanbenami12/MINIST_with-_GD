# MINIST_with_GD
 



MNIST consists of 60,000 handwritten digit images of all numbers
from zero to nine.

Each image has its corresponding label number representing the number in image In MNIST, each image contains a single
grayscale digit drawn by hand. And each image is a 784 dimensional vector (28
pixels for both height and width) of floating-point numbers where each value
represents a pixel’s brightness.



The MNIST database is a
dataset of handwritten digits of all numbers from zero to nine.

It has 60,000 training samples, and 10,000 test samples. Each image is
represented by 28x28 pixels 784-dimensional vector, each containing a value 0 - 255 with its
grayscale value 



 





It is a subset of a larger
set available from NIST.



The digits have been
size-normalized and centered in a fixed-size image.



It is a good database for
people who want to try learning techniques and pattern recognition methods on
real-world data while spending minimal efforts on preprocessing and formatting.



There are four files
available, which contain separately train and test, and images and labels.



 



Pre-processing 





We know that the
pixel values for each image in the dataset are unsigned integers in the range
between black and white, or 0 and 255.



 



 



We don't know the best
way to scale the pixel values for modeling, but we know that some scaling will
be required.



A good starting point
is to normalize the pixel values of grayscale
images, e.g. rescale them to the range [0, 1]. 



This involves first
converting the data type from unsigned integers to floats, then dividing the
pixel values by the maximum value



 





 



Normalize result will be 0.1307 and 0.3081, respectively.



We have done a pass on
the dataset and calculated per-channel mean/std, and we quite often use it on many
datasets to rearrange them to [-1, +1]. 

We apologies if this was confusing.



Increasing the
dimension by 1 and adding a bias weight and converted our problem from:



 





 



To:



 





 



 



Now we select only a specific digit from the MNIST dataset to turn
the above problem to binary.



 



We did it by making a mask for our real data set with 3 options:



 



1. Get the digits 0 to 4
against digits from 5 to 9.



2. Get even digits
against odd digits.



3. Get prime number
against the rest.



 



We chose our loss convex
function to be hinge loss form Lecture 5 (Stochastic Optimization)



Hinge lose - .



 



For an intended output [-1,
+1] and a classifier score y, the hinge loss of the
prediction y is defined as:





 



Hinge loss given by  is
1-Lipschitz.



So to get 1-Lipschitz. 

Suppose we have a neural network f composed of fully 784 connected layers,
convolution layers, and commonly used activation functions.



By applying Spectral
Normalization to the fully connected layers and the convolution layers, we
bound Lip(f) from above by 1 and D=784.



Ones we defined our
loss function we can find all parameters of our problem.



 



 



 





 



Notice:





We think that
constrained GD is projected GD.



 



Parameters: 



 



We bounded w, in all the cases above with a ball in R =1.



Extraordinary is GD, w
is not bounded in GD.



Then we need to calculate   using  m =5000.



We searched at previous
lectures, respectively:



1.   



2. 



3.  



4. 



 



 



 



 



 



 



 



 



Remarks:



·       
1 is from lectures 4





·       
2 is form lectures 4





·       
3 is from lectures 7



 





 



·       
4 is from lectures 8







Once we finished to find the parameters, we were ready to run the data
set.    



                                         



 



Run experiment:



We repeat the
experiments 10 times, by considering different random partitions. 



In our graph we can see
the average behavior for training optimization error (loss) in number of
iteration m and  
and for making it more simple we merged all the graphs together.



 



 



                                           
Digits 0 to 4 against digits from 5 to 9.



 



 



 



 











                       Even digits numbers
against odd digits numbers





 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



                                        Prime digits number against the rest



 




 


  
   
  
  
   
   
  
 

 



 



 



                                                                                                                   



 



 



 



 



 













 



We improved the
training time experiment with different learning rates.  



We did it by reducing
the learning rates and it causes a noise reduction in our graph. 



Then we increased the
step size that caused decreasing the loss and it's improved our training rate.



We can see it in the
figure below.



 




 


  
   
  
  
   
   
  
 

 

Original parameters                                                          
After minor the learning rates 
     

                                 




 


  
   
  
  
   
   
  
 

 

                                   After reducing the learning rates and increase the step size  




Conclusions:



We got Our Conclusions By looking at graphs
and theory:



 



1.
GD- w is not bounded in GD, we can reduce the learning rates as we wish without
prejudice the quality of the graph, only improve quality graph, so we got the
best loss.



2.
Constrained GD- w is bounded by a ball in constrained GD, from that we have convergent
loss.



3.
Regularized GD- w is bounded by a ball in regularization GD, from that we have convergent
loss to, but when we add the regularization to GD our loss will increase.



4.
SGD – We take a random input with probability which learns about a single example
at each stage and it makes more noise. We got the worst loss from the rest.



 



 



 



 



 



 



 



 



 



 



 





 



 





 



We
divide our dataset to train and test and repeat all the experiment but with
minor changes. 



1.
We took the optimal parameters with minor changes:



  



 



 



2.
Plot test error.  



3.
For plot classification error we used the binary method (if we detect correctly
the result is 0 if not, the result is 1) for the following options:



A. Get the digits 0 to
4 against digits from 5 to 9.



B. Get even digits
against odd digits.



C. Get prime number
against the rest.



 



4.
Test error makes changes with SGD and plot smoother shape against the train
error.



 



In the previous part we got a noisy
graph in SGD, so we tried to minimize the noise by changing the parameter (we will present this later in our
project file) and we got:



 



Test error before
optimal parameters 





 



 




 


  
   
   
   
   
  
  
   
   
   
   
  
  
   
  
 

 

        Test error with optimal
parameters                                               Training error

 



 



 



·       
We calculate the test error, from
completely disjoint data sets that makes our graph smooth.



 



Run experiment:



We will run our experiment now:



 




 


  
   
  
  
   
   
  
 

 

                                     Digits 0
to 4 against digits from 5 to 9








 


  
   
   
   
   
  
  
   
   
   
   
  
  
   
  
 

 

                               Even digits
numbers against odd digits numbers

 



 



                     



 



                                        Prime
digits number against the rest




 


  
   
   
   
   
  
  
   
   
   
  
  
   
   
  
  
   
  
 

 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



We improved the test
time experiment of with different . 



We did it by increasing
the 



 



 




 


  
   
   
   
   
  
  
   
   
   
  
  
   
   
  
  
   
  
 

 

Original parameters                                                                      
Increase the  

 



Original
parameters                                                            
Increase the  
 


  
   
   
   
   
  
  
   
   
   
   
  
  
   
  
 

 

 

 



·     
Increasing  makes fast error performance.



 



 



 



 



We improved the test time experiment of with different learning rates.



We did it by reducing the learning rates. 



Then we increased the
step size that caused decreasing the loss and it's improved our test error.



 



We can see it in the
figure below.



 



Original
parameters                                                      
After reducing the learning
rates       
 


  
   
   
   
   
  
  
   
   
   
   
  
  
   
  
 

 



               



 



               After reducing
the learning rates and increase
the step size   




 


  
   
  
  
   
   
  
 

 



 



 



 




 


  
   
  
  
   
   
  
 

 

Original parameters                                                      
After reducing the learning
rates 



 



 



              After reducing
the learning rates and
increase the step size   
 


  
   
  
  
   
   
  
 

 

 

 



 



 



 



·       
Reducing the learning and
increase the step size, make our loss less noisy.



 



 



 



 



 



Then we improvedexperiment with different learning rates by
increasing the  without getting overfitting   



 



 



                                                         
Original parameters 
 


  
   
   
   
   
  
  
   
   
   
   
  
  
   
  
 

 

 

 









 




 


  
   
  
  
   
   
  
 

 

                                                             Increase the 

 



·     
Increase the  improve
optimization without prejudice generalization.



Conclusions:



1. GD - giving the best performance.



2. - Mid-performance. 



3. -  
Helps to deal with overfitting issues.



4. SGD -If we get overfitting SGD help us to deal with its' issues.



And after changing
the optimal parameters, its' performance has
better result over .



5. The theoretical parameters give us a good bounded but not
necessarily give us good converge performance.



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 



 







We need to get the optimal empirical risk. 



We need to get L-Lipschitz and the bounded ball w,   and
T for bounded m.



 



 



 



The definition for GD:



From above:





From the paper 3.4 Discussion of the upper bounds: examples
of specific instantiations (Page 13)





 



Merging 1 and 2 (T in ) and we got:





For bounded m we take 3 for here





Then we got:





 



Conclusion:



1. 



2. 



3. 



 



 



 



 



 



Definition for SGD:



From lecture 8 page 3:





 For SDG we get different
bounded from GD 





And for GD is:





 



 



In GD
each iteration performs work for all available samples and it's affecting on
the running time




Unlike,
SGD get random input with probability, which learns about a single example at
each one stage that makes our running time to be faster. 



 



 





We
defined the optimal  by using our
MNIST data set and hinge loss on several instance.



Our
goal is to compare  against T In the
terms of running time.



We
take a random  between 0.01 to
10.



And
our T will be constant of 1000 samples. 





 



 



The test
and the classification have the same path.



The
optimal  ,after
several instance, is around 0.1.



 



 



 



Conclusion:



·     
High  gives us overfitting issues.



·     
Low  cannot converge.





 



                                                                   
GD



                                                            
Regularized GD 



 



 



 



 



GD and
Regularized GD is almost the same In terms of running time, but cannot converge the same points.



And
GD, again, has won 😊



 



 
