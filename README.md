# Location-Based-Restaurants-Recommendation-System
Using concepts of Big data Analytics a system is created to find restaurants based on reviews of food, location.

## Introduction 

Designed and implemented location based static and dynamic recommendation system for restaurants based on user input such as state, city, type of food.

## Problem Statement

People are sharing their experiences on products or services in the form of reviews, which enables other users for their decision making. It is hard for the user to go through each review, and it might mislead the user to use a wrong service or a product, if he/she goes by the review given by a user with opposite taste.


## Solution

To solve the above stated problem we are developing static and streaming recommendation system for the recommendation of the restaurants. Both the recommendation systems are built using Yelp academic datasets. Both static and streaming recommendation systems are User Input Driven. The trending top rated location specific restaurants information is provided by streaming recommendation systems.

## Approach

The Static Recommendation system is built on Apache Spark with Scala.
We are using ALS for Collaborative filtering for static data recommendation system.
The streaming recommendation system is based on the ratings and user’s current location.

## Size of data
<table>
  <tr>
    <td></td>
    <td align="center">Rows</td>
    <td align="center">Size</td>
    <td align="center">Description</td>
  </tr>
  <tr>
    <td align="center" width=175> Businesses </td>
    <td>229,222</td>
    <td>32MB</td>
    <td>Info of businesses</td>
  </tr>
 
  <tr>
    <td align="center" width=175> User </td>
    <td>686,557</td>
    <td>159MB</td>
    <td>Users</td>
  </tr>
  
  <tr>
    <td align="center" width=175> Reviews </td>
    <td>9,275,055</td>
    <td>1.8GB</td>
    <td>By users</td>
  </tr>
  
  <tr>
    <td align="center" width=175> Check-in </td>
    <td>61,050</td>
    <td>14MB</td>
    <td>Timings</td>
  </tr>
  
  <tr>
    <td align="center" width=175> Tip </td>
    <td>667,238</td>
    <td>79MB</td>
    <td>Derived from reviews</td>
  </tr>
</table>

## Tools and Technologies used

- PySpark with Streaming and MLLib(ALS)
- Python (as Kafka Producer/Consumer)
- Apache Kafka
- Zookeeper
- Scala (Removing unnecessary attributes)
- Elasticsearch(for storing JSON file)  
- Kibana (for visualization)

## Implementation

### Static Recommendation

 Static recommendation system is rating driven as reviews/ratings play a key role for choosing the best service or product. It recommends top 5 restaurants in a city to the user based on the type of food, city and state entered by user. The system is built on Apache Spark with Scala. 
 
### Working of Static Recommendation system

- Take the input from the user,
- Input: City, State, Category of food
- Based on the input, filter the business data file
- Find out the relevant restaurants based on the input by user, let’s call them Target Restaurants
- Now, get the data from review file which contains the ratings or reviews given to the restaurants.
- Join Target Restaurants with reviews
- Build an ALS Matrix comprising of users who have reviewed the target restaurants. This data is is used as a training data
- Test data: current user, list of restaurants
- Test and predict ratings in the required food category for the current user
- Return top 5 restaurants based on the average rating

### Streaming Recommendation System

Streaming recommendation system is based on the current ratings of the restaurants so that we can get the updated recent information about the food quality. So we are judging the restaurants based on its current performance not its previous rating, which is helpful for both user and business providers.Recommends top 5 TRENDING restaurants in a city(Las Vegas) to the user based on user location and the type of food entered by user.The system is built on Apache Spark with Scala.

### Working of Streaming Recommendation System

- Filter the Business Data (for city, star, Business_id, categories, name, stars, state, full_address, latitude and longitude) and Tips Dataset (for Business_id and Text).
- Join the Business Data with Tip Data and write the output to a csv File
- Read this output file by kafka producer written in python.
- This Program acts as a Producer and we are simulating the Streaming Process
- The Data is sent to the kafka consumer and thereby processed with  PySpark.
- Later the data is sent to Elasticsearch
- Using this data we can visualize using Kibana

## Results

### Static Recommendation system
The result of the Static Recommendation System is displayed here which consists of the top five restaurants obtained using the ALS model. The restaurant along with the predicted rating is shown below.

![image](https://user-images.githubusercontent.com/64421366/166134774-199ffad7-ca2f-4fa3-bfd4-8d1eda3208b7.png)

![image](https://user-images.githubusercontent.com/64421366/166135266-32fb456e-e6ad-41cc-b09f-5636d72c894d.png)


### Streaming Recommendation system

In results of the Streaming Recommendation System  , output has changed every time the data is streamed, which means that the user is being recommended differently for each new data stream which says that daily reviews on a particular restaurant change and the user will be recommended the best restaurants based on that day review.

![image](https://user-images.githubusercontent.com/64421366/166134879-977f1efb-3667-467c-808f-ee6fbf2142d8.png)

![image](https://user-images.githubusercontent.com/64421366/166134886-19b3980a-d3da-4cff-8737-d1818c38ec84.png)

## References 

- https://en.wikipedia.org/wiki/Apache_Spark
- https://www.elastic.co/products/elasticsearch
- https://en.wikipedia.org/wiki/Apache_Kafka
- https://www.elastic.co/products/kibana
- https://zookeeper.apache.org/

## Contributors

- Members : [Krina Khakhariya](https://github.com/Krina-521), [Arti Singhal](https://github.com/arti-13) and [Krunal Savaj](https://github.com/klsavaj)

