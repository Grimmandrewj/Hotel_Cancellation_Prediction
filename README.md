## Hotel Cancellations Analysis Project
Collaborators:  Hampton Hughes, Andrew Grimm, Fekadu Habeteyohannes, Brielle Bernardy, Karen Fan

## Dataset
For this project, we analyzed data concerning cancellations of hotel reservations in Portugal which we found at Kaggle.com: 
https://www.kaggle.com/datasets/ahsan81/hotel-reservations-classification-dataset?resource=download

This dataset consisted of information relating to the reservations such as number of adults and children, weekend and week nights, type of room reserved, lead time between the date the reservation was made and the first day of the hotel stay, repeat guests, number of previous cancellations and bookings, average room price, and more.  These cancellations can lead to a significant business interruption for the hotel especially if they take place at the last minute.  We set out to explore which factors are useful for predicting whether a booking will result in cancellation or not.  

## Methodology
Our review of the dataset confirmed that this analysis would be a classification problem as we would be predicting whether a hotel booking would be canceled or not based on the indicator column from the data.  As such, our target for the analysis was “booking_status” (canceled or not canceled).  The features consisted of no_of_adults, no_of_children, no_of_weekend_nights, no_of_week_nights, type_of_meal_plan, required_car_parking_space, room_type_reserved, lead_time, arrival_month, market_segment_type, repeated_guest, no_of_previous_cancellations, no_of_previous_bookings_not_canceled, avg_price_per_room, no_of_special_requests.

We decided to utilize two models for our analysis: Nearest Neighbors and Random Forest.  We preprocessed the data by creating a SQLite database and creating a Pandas DataFrame from the database.  We removed the booking_id, arrival_month, and arrival_date columns as we deemed them inconsequential for our analysis. 

We then split the data into training and testing data and scaled it using StandardScaler.  We created a function first to test the scaled data with the Nearest Neighbor model using varying values for N (5, 4, 3, 2, and 1) and plotted the results.  We then created the same function to test the data with the Random Forest model using varying numbers of estimators (100, 200, 300, 400, 500) and plotted those results.

## Results and analysis
With the Nearest Neighbor model, the balanced accuracy score was consistent, only varying betwen 82.8% and 83.8%.  The results varied slightly with each optimization, but remained in that range, with N = 4 returning the most accurate results:

![image](https://github.com/Grimmandrewj/Hotel_Cancellation_Prediction/assets/120341249/984587d5-6403-4eda-9702-72ec14e8f4d5)


| N_Neighbors  |  Balanced Accuracy Score |
| -----------  |  ----------------------- |
|      5       |           82.8%          |
|      4       |           83.8%          |
|      3       |           83.2%          |
|      2       |           83.3%          |
|      1       |           82.9%          |

The Random Forest model performed slightly better and maintained a very consistent level of accuracy regardless of the number of estimators, only varying between 87.3% and 87.5%.  The model was the most accurate with estimators = 200: 

![image](https://github.com/Grimmandrewj/Hotel_Cancellation_Prediction/assets/120341249/cc031224-6d1d-4776-80a9-83e20ae30f41)

| Estimators   |  Balanced Accuracy Score |
| -----------  |  ----------------------- |
|      100     |           87.46%         |
|      200     |           87.54%         |
|      300     |           87.49%         |
|      400     |           87.33%         |
|      500     |           87.35%         |

Overall, both models performed well, but the Random Forest model yielded more accurate results for this dataset.  We would recommend that the Random Forest model be used to test the prediction as it performed consistently well throughout all of the iterations and optimizations.  Since the difference in results was minimal, using 100 estimators appears to be the most effective solution as the accuracy was consistent and it completed the analysis more quickly.  In all attempts, the top three features that contributed to the cancellation prediction in order of importance were (1) lead time, (2) average price per room, and (3) number of special requests: 

![image](https://github.com/Grimmandrewj/Hotel_Cancellation_Prediction/assets/120341249/2cf8374e-e5b6-42af-a4c1-f98007da2efd)

We feel it is logical that the lead time would be an important datapoint since guests' plans for travel are more likely to change the further it is from the date of their stay.  However, it was somewhat surprising that it was consistently the most important category by nearly double with each optimization.  

Overall, both models provided a fairly accurate prediction for whether a booking would be canceled or not, but depending on the needs of the hotel and the importance they place on this prediction, further analysis may be needed since the results did not exceed 90% with either model.  These results would fall under the "good" bucket (rather than "very good") according to https://stephenallwright.com/balanced-accuracy/: 

![image](https://github.com/Grimmandrewj/Hotel_Cancellation_Prediction/assets/120341249/b52744b3-0a8d-4758-bb8a-3173fe62cd19)

However, according to https://www.obviously.ai/post/machine-learning-model-performance#:~:text=Good%20accuracy%20in%20machine%20learning,also%20consistent%20with%20industry%20standards, these are great results that fall within industry standards: 

*Good accuracy in machine learning is subjective. But in our opinion, anything greater than 70% is a great model performance. In fact, an accuracy measure of anything between 70%-90% is not only ideal, it’s realistic. This is also consistent with industry standards.*

Therefore, the level of confidence in these results would ultimately be up to the interpretation of the stakeholders.
  





