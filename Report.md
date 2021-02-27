### 1. Introduction
　　Recent years as the Internet develops,many interesting contents can be accessed easily.For example,comics and games.When it comes to comics,many people may have Japan in their 
mind.

<div align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/image/naruto.jpg" width = 600 />
</div>

　　Japan has become one of the most popular countries in the world by its high quality industrial products and its unique culture.In the year 2019,the total foreign travelers 
in Japan is about 32 million.Under this background,I want to make some information for all the people who are interested in Japan by grouping several Japanese major cities into 
different types.Hope this project will help when you want to make commercial recommends about traveling or selecting a favorite place to live in Japan.
<div  align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/image/どうぶつの森.jpg" width = 600 />
</div>


### 2. Data Requirement
　　There are 47 prefectures in Japan.I plan to take their 47 capital cities out and explore their commons and differences.Since it's not a big deal I will just list them out 
instead of scraping.Then by using API I can get the coordinates and explore them to get their recommended venues.I noticed query using explore without any other keyword limits,it will have a bad effect on the result,so I will also try other keywords to retrive the result to get better features.At last,I will use K-Means to figure out if the cities are more like or different from each other and compare which of the two different methods is better.

### 3.Methodology
#### 3.1 Data Preparation
1. First,my purpose is to cluster 47 major cities I just list them out manually.
2. Second,get coordinates information using Geopy API.

#### 3.2 Data Analysis
1. Visualise the data features and think the feature catogory is a good one to cluster cities as it contains the recommendation info and may indicate what kind of place this city is.
As for other features such as latitude,longitude are less important for Japan doesn't have an extreme development unbalance among different parts.So I just dropped them.
<div  align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/nagoya_data.png" width = 600 />
</div>

2. At first I used the default parameter of radius with 500,which did good in previous lab assignments.However,after several tries,I found that many cities are clustered into wrong groups,after analysis I realized radius with 500 is too small and the coordinates got by API doesn't return the central position of a city.So many cities lost their important information,in order to avoid this I expanded the radius to 5000 and finally got a better result.
3. The catogory feature is a text information which can't be used directly for machine learning,in order to make it useful,I used one-hot encode to deal with it.Then use pandas group function to get the final averaged grouped data.
<div  align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/image/grouped_data.png" width = 600 />
</div>

4. Since the problem is to cluster the cities,with good features K-Means can manage it so I chosed it.

### 4.Result
1. I used features abstracted by previous steps,what I got is not a satisfying result.I got apparently cities with historic cities and other cities clustered into the same group.And got 2 groups which I failed to tell the difference between them.What's more Tokyo and Kyoto are grouped as the same with some rural cities.It's unacceptable.
<div  align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/image/wrong_group.png" width = 600 />
</div>
<div  align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/image/result_1.png" width = 600 />
</div>
2. After analysis I found the features I got are not good.I just abstracted the features using a query which will retrive all the places can be found in the database without 
any other considerations.For example,when comparing a traveling city and a industrial city,of course both will have reataurants and convenience stores and hotels,the 
difference is a traveling city will have more popularity on tour spots.So to get better features,I have to consider this,and use section=topPicks keyord which will 
retrive a mix of recommendations and sortByPopularity keyword to sort the results by popularity.After doing in this way,I got a relatively acceptable result.
<div  align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/image/right_group.png" width = 600 />
</div>
<div  align="center">    
<img src="https://github.com/Ambiyang/Coursera_Capstone/blob/main/image/result_2.png" width = 600 />
</div>

### 5.Discussion
1. The most important thing I noticed is the information you can get from API is very important.If you are working with wrong information,you get wrong results.How to retrive correct information is important.In this project,all the features share the same weight,it's not good.For every city has restaurents and hotels and Ramen shops.What makes them different is their key features like historic sites or park(It's the case of Tokyo).In order to use these key features in K-Means,I just ordered them and used less features for input like 5 instead of 10.
2. If you don't want to miss the least information you can get,you may try other algorithms which can re-weight different features.For example,you want give more attention to features like castle,park,Chinese restaurant(which means more foreigners).What k-Means does bad is it taking them in a same weight.It won't cluster 
 good because it's not using the features in a good way.
 
### 6.Conclusion
　　Through this work, I realised that there are so many information can be used to make wonderful things,maybe someday I will try to make a new product using the ideas I got in this lab.Perhaps there are people think these information doesn't tell important things,for we knew it by common sense.That may be true,but it deponds.Before taking data science course I thought in that way,but as I learning I found it not true.It depends on how you use there information.  
　　Thus,while studying new technologies being a creative person is the same important for skills can be aquired if you work hard but ideas not.Remember trying to use data to solve problems is a start.If you just learnt data science and don't think in a data scientist's way,you learnt nothing.That's not what we want to see.So,maybe try to change our mind is the same important.
