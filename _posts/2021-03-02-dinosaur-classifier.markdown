---
title:  "Dinosaur Classifier"
subtitle: "An image classifier 65 million years in the making."
image: "images/dino.jpg"
imagebg: "images/bg_dino.jpg"
date:   2021-03-03 00:00:00
layout: post
---

I was born in the year Jurassic Park was released and when I was 4 years old the US 
remake of Godzilla was distibuted. This means that as a child, like many of my 
generation, I was obsessed with large reptiles! Back in the day I was a bit confused 
about the different types of dinosaurs (T-rex, brontosaurus, stregosaurus, triceratops),
which is why today I have developed an image dinosaur classifier that can also recognize
the king of monsters from prehistoric reptiles.

### In the beginning was the Data

The first thing you need to do in order to train a classifier is to collect data.
 Unfortunately, the public datasets focus much more on irises than dinosaurs, 
 which is why I decided to build the training set with data extracted 
 via a web scraper.

To use it, you can use my notebook available [here.](https://github.com/glep93/google_image_scraper/blob/main/Scrap%20images.ipynb)

The web scraper search on google the dinosaur and save all images related to it. All this 
images will be labelled as the search string. This means that an image found searching 
the world 'T-rex' is classified as 'T-rex'.

### The classifier

Developing a classifier from scratch is definitely something very elegant, but transfer 
learning nowadays is the best and fastest way to create an image classifier.

The architecture of this model is very simple, the first non-drawable layer extracts the
 main features of the image and is taken from 
 [here](https://tfhub.dev/google/tf2-preview/mobilenet_v2/feature_vector/4),
 while a second dense layer is trained to identify the different classes 
 (T-rex, brontosaurus, stregosaurus, triceratops and Godzilla) to which the image belongs.
 
 Once the model was trained, I just download it and use on the web app. You can find the
 colab notebook of the model [here](https://colab.research.google.com/drive/1F0MHvQg_WqShmLh7J-fIgEvJQM-AjRb-?usp=sharing)
 
### The web app

Streamlit is one of the latest frameworks for creating apps in python. Its philosophy is 
to develop apps the same way you write plain Python scripts. 

The web app will read the uploaded image, then the classifier trained before will give its
prediction. At this point the user can say what the correct answer is and update the confusion matrix of the model.

The complete app can be found at [dinoclassifier.ml](http://dinoclassifier.ml).


 