---
title: "League Data Visualiser"
description: ""
date: 2024-04-28 21h:00:00 -0000
categories:
  - Other
tags:
  - Programming
published: true
img_path: /assets/
---

## **Optimizing Game Strategies: Leveraging Data Analytics in League of Legends**

### **Project Overview**
In an ongoing effort to improve strategic decision-making in League of Legends, myself and a friend began developing the LeagueDataVisualiser. This tool aims to analyze various game factors such as kills, tower destruction, and other objectives to determine their impact on the outcome of the game.

### **Development Progress and Goals**
We are transitioning our data handling from JSON to a more robust database design, and incorporating data from multiple player IDs. Our to-do list includes tasks such as:
- Designing database schemas for different statistical data.
- Deciding on the exact datasets to collect, including game events like first blood, tower kills, and dragon captures.
- Implementing logistic regression and other predictive models to analyze game data.

### **Technical Implementation**
#### Data Collection
Using Python, we have scripted interactions with the Riot Games API to fetch match details. These details are stored in a MongoDB database, ensuring that we only add new matches to avoid duplicates.

![API Interaction Diagram]()

#### Data Preparation and Analysis
Data fetched includes various objectives achieved by each team during the match. We have structured this data into a Pandas DataFrame for detailed analysis.

![Data Structure Overview]()

#### Predictive Modeling
With the data prepared, we employed a Logistic Regression model, trained to predict match outcomes based on various game statistics. This involves:
- Selecting relevant features such as kills, dragon captures, and tower destructions.
- Splitting the data into training and testing sets.
- Standardizing the features to scale for better model performance.

### **Insights and Interpretation**
Initial model evaluations show promising accuracy in predicting match outcomes. The model's coefficients provide insights into which factors most significantly influence a win or loss, guiding players on strategic focuses.

![Model Coefficients Chart]()

### **Visualization and Reporting**
We plan to use visualization techniques like heatmaps and scatterplots to present these insights effectively. These visualizations will help in understanding the relationships between game factors and match outcomes.

![Heatmap of Game Factors]()
![Scatterplot of Critical Moments]()

### **Future Directions**
The next steps involve refining our model with more data and exploring other machine learning techniques such as XG Boost. Additionally, we aim to publish our findings and insights through comprehensive articles.

### **Conclusion**
By leveraging detailed match data and advanced analytics, the LeagueDataVisualiser seeks to empower players and teams in League of Legends with data-driven strategies that enhance their gameplay and decision-making.

![Final Presentation Slide]()
