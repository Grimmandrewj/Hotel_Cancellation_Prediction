## Hotel Cancellations Analysis Project
Collaborators:  Hampton Hughes, Andrew Grimm, Fekadu Habeteyohannes, Brielle Bernardy, Karen Fan

## Dataset
For this project, we analyzed data concerning cancellations of hotel reservations in Portugal which we found at Kaggle.com: 
https://www.kaggle.com/datasets/ahsan81/hotel-reservations-classification-dataset?resource=download

This dataset consisted of information relating to the reservations such as number of adults and children, weekend and week nights, type of room reserved, lead time between the date the reservation was made and the first day of the hotel stay, repeat guests, number of previous cancellations and bookings, average room price, and more.  These cancellations can lead to a significant business interruption for the hotel especially if they take place at the last minute.  We set out to explore which factors are useful for predicting whether a booking will result in cancellation or not.  

## Methodology
Our review of the dataset confirmed that this analysis would be a classification problem as we would be predicting whether a hotel booking would be canceled or not based on the indicator column from the data.  As such, our target for the analysis was “booking_status” (canceled or not canceled).  The features consisted of no_of_adults, no_of_children, no_of_weekend_nights, no_of_week_nights, type_of_meal_plan, required_car_parking_space, room_type_reserved, lead_time, arrival_month, market_segment_type, repeated_guest, no_of_previous_cancellations, no_of_previous_bookings_not_canceled, avg_price_per_room, no_of_special_requests.

We decided to utilize two models for our analysis: Nearest Neighbors and Random Forest.  We preprocessed the data by creating a SQLite database and creating a Pandas DataFrame from the database.  We removed the booking_id, arrival_month, and arrival_date columns as we deemed them inconsequential for our analysis. 

We then split the data into training and testing data and scaled it using StandardScaler.  We created a function first to test the scaled data with the Nearest Neighbor model using varying values for N (5, 4, 3, 2, and 1) and plotted the results.  We then created the same function to test the data with the Random Forest model using varying numbers of estimators (500, 400, 300, 200, and 100) and plotted those results.

## Results and analysis
With the Nearest Neighbor model, the accuracy of the results generally increased as the value for N decreased:

![image](https://github.com/Grimmandrewj/Hotel_Cancellation_Prediction/assets/120341249/f8b2cadc-1e41-4aae-ac24-61f3ff7c45f3)

| N_Neighbors  |  Balanced Accuracy Score |
| -----------  |  ----------------------- |
|      5       |           86.8%          |
|      4       |           94.9%          |
|      3       |           92.7%          |
|      2       |           95.9%          |
|      1       |           98.5%          |

With the Random Forest model, the results maintained an extremely high level of accuracy regardless of the number of estimators: 

![image](https://github.com/Grimmandrewj/Hotel_Cancellation_Prediction/assets/120341249/9ddd357c-bc5c-40e3-91ba-bd26dc5e441d)

| Estimators   |  Balanced Accuracy Score |
| -----------  |  ----------------------- |
|      100     |           98.79%         |
|      200     |           98.74%         |
|      300     |           98.79%         |
|      400     |           98.78%         |
|      500     |           98.79%         |

Overall, both models performed well, but the Random Forest model yielded very strong results for this dataset.  We would recommend that the Random Forest model be used to test the prediction as it performed extremely well throughout all of the iterations and optimizations.  Since the difference in results was minimal, using 100 estimators appears to be the most effective solution as it yielded excellent results and completed the analysis more quickly.  In all attempts, the top three features that contributed to the cancellation prediction in order of importance were (1) lead time, (2) average price per room, and (3) number of special requests.  





