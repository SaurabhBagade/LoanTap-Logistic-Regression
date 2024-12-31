## Insights


1. The data is pretty big for analysis. Around 4 lakh rows.
2. Extracting the ZIP code from the address shows only 10 zip codes. Meaning the data is from selected areas. After this we drop the address column.
3. Converting the term column to numerical after extracting from string.Same for employee length.
4. The data is imbalanced in terms of target variable - loan_status. The data is 80-20 imbalance.
5. Both pearson and spearman correlation shows are high collinearity of 0.95 in loan_amnt and installment. So we dropped the installment.
6. The home_ownership has 2 categories which carry very less data so we convert them to OTHER.
7. The grade column is converted to category type with the order precedence.
8. The subgrade column is converted to category type with the order precedence.\
9. The verification column is converted to category type.
10. Both earliest_cr_line and issue_d are converted to date type and we extract month and year from it. After extracting month and year we drop the previous columns.
11. The purpose has 10 categories so we convert it to category type without any precedence.
12. The title and emp_title have too much cardinality and too many spelling mistakes so we drop them.
13. We convert initial_list_status and application_type to category.
14. For removing outliers from revol_util we use IQR.
15. The pub_rec_bankruptcies has very less na values so we drop the na rows.
16. For emp_length we use KNNImputer as it guarantees the data does not become bias and also it considers other features also.
17. The mort_acc cannot be directly imputed so we use the group by values of its mean by total_acc.
18. As other features has too many outliers we can lose data so we only remove outliers from selected columns  ['loan_amnt','int_rate','dti', 'revol_bal','revol_util'] 
19. Certain zip codes are where all loans are cleared but there are also areas where loan is not cleared. This shows that zip code may have a greater impact on the model.
20. Employees with 10 or more year of experience are clearing the loan more compared to others
21. Clearly The grade A,B and C have the highest loan paying .The grade G has none or near 0 
22. The sub-grade B2, B3 and B4 are the highest number of loan cleaners. The sub-grade C3, C4 and C5 are the highest number of loan defaulters.
23. The loan defaulters generally go for higher loan term
24. There is no significant diff in loan amount as per loan status
25. If the person has a mortgage property the loan is more likely to be paid
26. Higher the grade the loan has higher chances of getting paid
27. Higher the subgrade the loan has higher chances of getting paid
28. Joint accounts have higher chances of getting paid
29.  Target encoding of categorical columns (I have included zip code, year and month as they also have limited categorical values and are not continuous with more numbers). Target encoding should only be applied to category or object dtypes, it won't work on continuous data types like int or float. In our dataset zipcode is an object and not int or float.
30. The model with all features and no over sampling has a score of 88.8%. With the help of ROC-AUC curve we can use a threshold value of 0.2.
31. We drop the columns which have a VIF score > 12. This ensures that the data does not have multicollinearity
32. We again train the model with only the features that are not multicollinear. This gives us the same score as multicollinearity only affects analysis and not the model prediction.
33. As the data was imbalanced 80-20 we needed either over or under sampling. We chose SMOTE as it ensures that the data is not repeated. SMOTE also introduces new data points to balance out the two categories
34. We get a lesser model score after SMOTE because the data is more balanced. Both the classes are pushing the boundary away from each other leading to a balanced line of separation
35. Zip code has the highest impact on loan clearing, this indicates that localities with higher status are where people take more loans and also clear them.
36. The final trained model comes up with a score of 85.2% which is OK. We can also so polynomial regression so as to increase the model performance.


## Recommendations


1. The concentration of loans in the B, C, and A categories suggests these grades are most common and potentially the most reliable segments.
2. The long employment duration of many borrowers indicates stability, which is a positive sign for lenders. The primary purpose of loans being debt consolidation reflects a trend towards financial management and restructuring by borrowers.
3. Develop tailored loan products for the most common borrower segments (B, C, and A grade borrowers) to enhance product-market fit.
4. Offer more flexible terms for higher-grade loans and consider stricter terms for longer-term and lower-grade loans to mitigate risk.
5. Continuously monitor and adjust credit scoring models in response to changes in borrower behavior and economic conditions.
6. ZIP codes where loan repayment is higher should be made easier for loan approval.
7. The bank should also make a single factor that they calculate for loan approval.