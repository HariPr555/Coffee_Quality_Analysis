# Coffee_Quality_Analysis
This report provides a detailed assessment of coffee quality through the use of Power BI, emphasizing the critical role of sensory attributes, coffee varieties, and processing methods. By analyzing these factors, the report uncovers their impact on cup point ratings and overall quality. The insights derived aim to guide producers in refining their practices and improving product consistency. Ultimately, this analysis supports the pursuit of higher quality standards in the competitive coffee market.

# Summary
![CQA_Summary](https://github.com/user-attachments/assets/4aca3c06-7173-40da-bfbf-12444b2ae8d6)

# Sensory Attributes Analysis I
![CQA_SAA_1](https://github.com/user-attachments/assets/f0696935-6a4a-4479-885e-17c3cff06db9)

# Sensory Attributes Analysis II
![CQA_SSA_2](https://github.com/user-attachments/assets/8a5e2fbb-3505-4ea6-b64b-60815ecede49)

# Sensory Attributes Analysis III
![CQA_SSA_3](https://github.com/user-attachments/assets/7750c544-1e3a-464c-8d7d-b24ccbec4304)

# Defect Analysis
![CQA_DA](https://github.com/user-attachments/assets/ff9a78bb-193a-41d8-a7a5-84ce3d439d73)

# Regional Analysis
![CQA_RA](https://github.com/user-attachments/assets/300941b2-5d26-408c-b22a-d0b951bdfc45)

# Adhoc Analysis
![CQA_AA](https://github.com/user-attachments/assets/0a688034-ba81-45a3-b724-f20931f91525)

# 1. Background
The Coffee Quality Institute (CQI) is a non-profit organization that works to improve the quality and value of coffee worldwide. It was founded in 1996 and has its headquarters in California, USA. CQI's mission is to promote coffee quality through a range of activities that include research, training, and certification programs. The organization works with coffee growers, processors, roasters, and other stakeholders to improve coffee quality standards, promote sustainability, and support the development of the specialty coffee industry.

# 2. Project Objectives
The primary goal of this project is to leverage the rich dataset provided by CQI to understand the factors that contribute to coffee quality. 
- Evaluate the key determinants of coffee quality by analyzing sensory attributes such as aroma, flavor, acidity, and aftertaste.
- Investigate the correlation between processing methods, origin regions, and coffee quality scores.
- Identify trends and patterns in defect occurrences and their impact on overall coffee quality.
- Analyze the interactions between different variables to understand their influence on Total Cup Points, which serve as an overall measure of coffee quality.

# 3. Technical Stacks

- Data Visualization Tool: Power BI
- Scripting : Python
- Data Source: CSV containing Coffee Quality data

# 4. Data Understanding
The Coffee Quality Data from CQI consists of 206 records and includes 31 features such as:
- Sensory Evaluations: Aroma, Flavor, Aftertaste, Acidity, Body, Balance, Uniformity, Clean Cup, Sweetness.
- Defects: Category One (visual defects) and Category Two (taste defects).
- Processing Methods: Washed/Wet, Natural/Dry, Pulped Natural/Honey, etc.
- Origin Information: Country of origin, harvest year, and coffee variety.


# 5. Data Preprocessing

- **Remove Empty Columns and Rows**: Identify and remove any empty columns and rows.
- **Remove Duplicates**: Deduplication of data to avoid redundancy.
- **Rename Columns**: Ensure appropriate names are used for better analysis.
- **Change Data Types**: Ensure columns have appropriate data types (e.g., dates, numbers, text).
- **Handle null values**: Replaced null values with “unknown”
- S**tandardize Values**: Replaced and formatted values to maintain data consistency.
- **Split Columns**: Create new columns to generate hierarchy for trend and pattern analysis.
- **Feature Selection**: Selected relevant features and dropped the irrelevant columns.
- **Feature Transformation**: Translated the columns that had Chinese text to English to maintain data consistency.


# 6. Data Modelling

- Created Fact and Dimension Tables
  - Fact Table: Coffee Sensory.
  - Dimension Tables: Coffee Manufacturing, Coffee Processing, Coffee Defects
- Established Relationship between Fact and Dimension Tables.
- Data Formatting
- Generate Hierarchies
- DAX

# 7. DAX
**Calculated Measures**:
- Sum of Cup points = SUM('Coffee Sensory'[Cup points])
- Sum of Total weight of Beans = sum('Coffee Processing'[Total Weight of Beans])
- Total Category One defects = sum('Coffee Defect'[Category One Defects])
- Total Category Two defects = sum('Coffee Defect'[Category Two Defects])
- Total Defects = sumx('Coffee Defect', [Category One Defects]+[Category Two Defects])
- Average Coffee Quality per KG = DIVIDE([Sum of Cup points], [Sum of Total weight of Beans], 0)

**Calculated Columns**:
- Total Weight of Beans = 'Coffee Processing'[Bag Weight in Kg]*'Coffee Processing'[Number of Bags]
- Altitude Range = SWITCH(TRUE(), 'Coffee Manufacturing'[Altitude]<500, "Below 500", 
                                  'Coffee Manufacturing'[Altitude]<1000, "500-1000", 
                                  'Coffee Manufacturing'[Altitude]<1500, "1000-1500", 
                                  'Coffee Manufacturing'[Altitude]<2000, "1500-2000",
                                  "Above 2000")
# 8. Report Visualization

# Summary Page Analysis
- **Grading Completion Status**
    - The gauge shows that 207 coffees have completed grading, indicating the extent of evaluated coffee samples. This status indicator helps assess the progress of the grading process in a batch of coffee samples.
      
- **Coffee Production in KG Over Time**
    - This line graph depicts the total coffee production (in KG) across time, with a decline from 13.1M KG in 2022 to 0.7M KG in 2023. The visual highlights fluctuations in production volume, which may signal environmental or market-related factors affecting production.
      
- **Category One and Two Defects Count**
    - The counts of coffee defects are shown for Category One (28) and Category Two (466). Category One defects include critical flaws like sour beans, while Category Two captures lesser issues. These figures are crucial for determining the overall quality and consistency of coffee batches.
      
- **Processing Methods Distribution across Countries**
    - This pie chart breaks down the coffee processing methods used in various countries. The most common method is Washed/Wet (124 occurrences), followed by Natural/Dry (46 occurrences). Other methods like Pulped Natural/Honey and specialized techniques (Anaerobic, Double Carbonic Maceration) are used less frequently.

# Sensory Attribute Analysis I
- **Comparison of Sensory Attributes with Total Cup points**
    - Shows how different sensory attributes correlate with the total cup points. Attributes like Flavor and Aftertaste show a strong positive correlation with overall cup points, while Uniformity has a weaker correlation.
      
- **Sensory Attributes Scatter plot**
    - These visuals show the relationship between total cup points and individual sensory attributes like Flavor, Balance, Aftertaste, and Acidity. The plots help identify patterns and strength of associations between sensory scores and overall performance.

# Sensory Attribute Analysis II
- **Variety vs. Total Cup Points and Sensory Attributes**
    - This table provides an overview of different coffee varieties and their corresponding total cup points and individual sensory attributes such as acidity, aftertaste, and aroma. This helps identify the highest-performing varieties based on different sensory criteria. For example, Castillo has the highest total cup points (89.33) and excellent performance in categories like Sweetness and Clean Cup.

# Sensory Attribute Analysis III
- **Processing Method vs. Total Cup Points and Sensory Attributes**
    - Double Anaerobic Washed and Semi-Washed methods produce the highest cup points, with strong sensory attributes in terms of sweetness, flavor, and body. The Semi-Lavado method, however, results in lower scores.

# Defect Analysis
- **Distribution of Category I and II Defects by Region**
    - North America has a high rate of Category II defects, indicating that their coffee could be impacted by factors like poor processing or post-harvest handling issues. Africa, despite its high quality, has significant Category I defects.
      
- **Total Defects vs Variety**
    - Caturra, Catuai, and Bourbon varieties show the highest defects. These popular varieties need more careful handling, especially in terms of post-harvest processes.
      
- **Impact of Defects on Total Cup Points by Processing Method**
    - There is a noticeable inverse correlation between defects and total cup points. As defects increase, total cup points decrease, especially for methods like Wet Hulling and Semi-Lavado.
