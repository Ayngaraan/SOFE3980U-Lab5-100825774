# SOFE3980U – Lab 5: Data Quality and Validation

## Task 1 – Great Expectations

**In your report, explain the three expectations you used and their relevance to the dataset.**

**Expectation 1: `expect_column_values_to_not_be_null` on `Timestamp`**  
Ensures no timestamps are missing. Every row must have a timestamp for the data to be usable in temporal analysis.

**Expectation 2: `expect_column_values_to_be_between` on `Car1_Location_X` (min: 0, max: 1920)**  
Validates that X-coordinates fall within the image width. Values outside this range are physically impossible and indicate corrupted annotation data.

**Expectation 3: `expect_column_values_to_be_in_set` on `Occluded_Image_view` (values: [0, 1])**  
Enforces that the occlusion flag is binary. Any value other than 0 or 1 indicates a labeling error.

---

## Task 2 – CleanLab: Mislabeled Point

**Why might this data point be mislabeled, and which feature values could have caused the misclassification?**

The flagged data point was labeled `<=50K` but had feature values strongly associated with high income — high education level, managerial occupation, significant capital gains, and long work hours. These features together made the model highly confident the true label should be `>50K`, suggesting the original label was a data entry error.

---

## Task 3 – CleanLab: Iris Anomalies

**1. Do these suspected anomalous data points match what you expect for their species? Why or why not?**  
No. The flagged points had measurements inconsistent with their labeled species — for example, petal dimensions that fall within another species' range entirely.

**2. Which feature (sepal length, petal length, etc.) seems most unusual in these points?**  
Petal length, as it is the most discriminative feature in the Iris dataset and provides the clearest separation between species.

**3. How can you check if these values are truly anomalies using the original dataset?**  
Compare the flagged values against per-species mean and standard deviation. A high z-score (>2–3) confirms the value is statistically unusual for that species. Plotting the points on a pairplot also makes outliers visually obvious.
