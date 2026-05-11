Business Description
My project focused on a fast-food restaurant, a McDonald's location, based on publicly available customer reviews. The business operates within the quick-service restaurant industry, characterized by high volume, standardized menus, and an emphasis on speed and convenience. Key aspects of its operation include drive-thru services, in-store dining, and potentially delivery services. Customer satisfaction is crucial for repeat business and maintaining brand reputation in a competitive market.
Review Dataset Description
The dataset comprises customer reviews sourced from Google Maps. It contains a total of 995 reviews, each including a star rating (1-5), the review text (snippet), date, user information, and other details like order_type, price_per_person, and details (food, service, atmosphere ratings). The reviews capture direct customer feedback on their experiences, encompassing various aspects from food quality and service speed to staff interaction and overall satisfaction.
Key characteristics of the dataset:
•	Total Reviews: 995
•	Rating Distribution:
1.0 Star: 411 reviews
5.0 Stars: 192 reviews
4.0 Stars: 137 reviews
3.0 Stars: 133 reviews
2.0 Stars: 122 reviews 
This distribution indicates a bimodal pattern, with a significant number of both very negative (1-star) and very positive (5-star) reviews, and fewer reviews in the middle range. This dataset is valuable for understanding customer sentiment, identifying pain points, and pinpointing areas of excellence.
Executive Summary
This report synthesizes findings from various text analytics techniques applied to Google Maps reviews for McDonald’s location. The goal is to extract actionable insights that can drive operational improvements and enhance customer satisfaction.
Data Loading and Initial Exploration 
The initial steps involved loading review data from Google Map Reviews API, inspecting its structure (reviews.columns, reviews.describe()), and visualizing the distribution of ratings. We also examined review length and its relation to 'likes'.

Meaning of Results
The reviews.describe() output highlighted that ratings vary widely, with a mean of 2.57. reviews['rating'].value_counts() confirmed a high number of 1-star reviews (411) and 5-star reviews (192), suggesting polarized customer experiences.
Review lengths vary, but generally longer reviews tend to be associated with lower ratings, implying customers might elaborate more when dissatisfied.
Business Application
 The bimodal distribution of ratings signals a need to investigate both extreme ends. Understanding why customers give 1-star versus 5-star ratings can help standardize positive experiences and mitigate negative ones. The correlation of longer reviews with lower ratings indicates a potential source of detailed feedback for critical issues.
Named Entity Recognition (NER)
 SpaCy's en_core_web_lg model was used to identify and categorize entities (e.g., PERSON, ORG, TIME) within the review snippets. Common words and numbers like 'mcdonald', 'one', and ‘15 minutes' were excluded to focus on more meaningful entities.
Meaning of Results
Initial NER revealed frequent mentions of 'McDonald', 'McDonald's' (as ORG), and numerical entities (like '2', '3', 'one', 'two'). Time entities like '20 minutes', '15 minutes' also appeared often.
More specific entities emerged, such as 'McChicken', 'Big Mac' (products), 'manager' (person), and specific time phrases ('5 minutes', 'midnight').
Business Application
Identifying frequently mentioned entities helps pinpoint specific aspects of the business that customers refer to. For instance, high mentions of 'McChicken' in reviews suggest that its quality or availability directly impacts customer experience. Frequent mentions of time-related entities ('15 minutes', 'night') indicate that service speed and operational efficiency at specific times are critical areas. Management can use this to focus on training, product consistency, and staffing at peak hours.






Sentiment Analysis 
Two sentiment analysis models were employed: VADER (rule-based) for compound sentiment scores and BERT (LLM-based) for categorical sentiment labels ('1 star' to '5 stars'). I analyzed the distribution of these scores and compared BERT's predictions against user-assigned star ratings.
VADER
The reviews[['sentiment_neg', 'sentiment_neu', 'sentiment_pos', 'sentiment_compound']].describe() output showed a slightly positive average compound score, but significant variation. The distributions indicated a high proportion of neutral sentiment, with positive sentiment being more prevalent than negative when emotional language was present.
BERT
 The BERT model provided explicit '1 star' to '5 stars' labels. The distribution showed a high frequency of '1 star' predictions. The heatmap demonstrated substantial alignment between BERT's predicted sentiment and user-assigned ratings, especially at the extremes (1-star and 5-star). Disagreement was most noted in the middle ratings (2-3 stars), where BERT tended to skew more negatively. 
Business Application
Sentiment analysis offers a quantitative measure of customer emotion. The VADER analysis suggests that most reviews are fact-based, but when emotions are present, they lean more positive. BERT's ability to directly classify sentiment into star ratings provides a robust validation of user ratings and can be used to automatically categorize new reviews. The observation that BERT skews negative for middle-range reviews suggests that even slightly critical language in 2-3 star reviews is strong enough for an LLM to interpret it negatively. This indicates that the business should pay close attention to any reviews that are not explicitly 4 or 5 stars, as they likely contain underlying dissatisfaction.
Topic Modeling (LDA) 
Latent Dirichlet Allocation (LDA) was applied to review snippets to uncover latent topics or themes. Stopwords, including custom ones like 'love' and 'mcdonald', were removed to enhance topic clarity. Topics were then assigned descriptive names and their distribution visualized.
Meaning of Results
The LDA identified topics with keywords such as:
o	Topic 1: ['food', 'order', 'drive', 'service']
o	Topic 2: ['get', 'minutes', 'wait', 'time']
o	Topic 3: ['customer', 'manager', 'staff', 'attitude'] 
These topics were descriptively named as 'Order and Service Experience', 'Speed and Delivery', and 'Product Quality - Food Items'. 
Business Application
Topic modeling provides a high-level understanding of what customers are talking about. If 'Speed and Delivery' is a highly dominant topic, it points to potential bottlenecks in operations. If 'Product Quality - Food Items' is prominent, it highlights concerns about consistency or specific menu items. This enables management to focus resources on improving specific areas identified as frequent discussion points in customer feedback.
Text Summarization (Extractive and Abstractive) 
Extractive summarization identified key sentences directly from the text, while abstractive summarization generates new, concise sentences capturing the main idea. 
Meaning of Results
Both methods effectively condensed review content. Extractive summaries provided direct quotes, useful for identifying exact phrases customers used. Abstractive summaries offered more fluent, human-like recaps.
Comparing summaries for the highest and lowest-rated reviews provided quick insights into what makes a review positive versus negative.
Business Application
 Summarization is invaluable for processing large volumes of feedback. Managers can quickly grasp the essence of many reviews without reading each one in full. This is particularly useful for quickly identifying recurring positive comments to replicate and critical issues that need immediate attention. For example, quickly seeing that positive reviews mention 'friendly staff' and negative reviews mention 'long wait times' provides immediate, actionable insights.
Text Classification 
A Logistic Regression model was trained to classify reviews as 'positive' (4 or 5 stars) or 'negative' (1 or 2 stars), excluding neutral (3-star) reviews. TF-IDF was used for feature extraction, and the model's performance was evaluated using a classification report.
Meaning of Results
•	The model achieved an overall accuracy of 77%.
•	The model was excellent at identifying all actual negative reviews.
•	When it predicted a review was positive, it was always correct.
•	The model struggled to identify all actual positive reviews, often misclassifying them as negative.
•	This imbalance in performance likely stems from the imbalanced dataset (58 negative vs. 24 positives in the test set).
Business Application
A text classification model can automate categorizing incoming reviews, allowing businesses to flag critical feedback for intervention quickly. While this model shows excellent recall for negative reviews (meaning few negative reviews are missed), its struggle with positive recall suggests that future models could be improved with more balanced training data or techniques like oversampling/undersampling. However, its strong ability to identify negative sentiment reliably is a significant advantage for proactive problem-solving.
Analysis of Negative Reviews: Topic Modeling and Named Entities 
The topics for negative reviews revealed core themes of 'order', 'food', 'go', 'minutes', 'get', 'drive', 'fries', and 'went'. These strongly indicate issues with order accuracy, food quality (e.g., 'fries' often mentioned in negative contexts), and speed of service, especially for drive-thru interactions.
The filtered entities from negative reviews highlighted specific mentions like 'manager' (PERSON), 'morning', 'night', 'lunch' (TIME), and product names. High occurrences of 'manager' in negative reviews could indicate escalations or unresolved issues.
Business Application
This targeted analysis is crucial for actionable insights. It confirms that the primary sources of customer dissatisfaction are centered around order fulfillment (accuracy, completeness), food quality (e.g., specific items like fries), and waiting times (especially drive-thru and during peak hours like 'morning', 'night', 'lunch'). Mentions of 'manager' suggest that these issues often require managerial intervention, pointing to potential front-line staff training gaps or empowerment issues. The business should prioritize addressing these specific operational challenges.
Interaction of Text Analytics with Numerical Data: Sentiment Analysis and Star Ratings
A clear example of text analytics interacting with numerical data is the comparison of BERT-predicted sentiment labels with user-assigned star ratings. 
The heatmap visually presents the numerical count of reviews that fall into each combination of user rating and BERT-predicted label. This is a direct cross-tabulation, a statistical method, applied to the output of a text analytics model.
Benefits for this business
The strong diagonal presence in the heatmap confirms that BERT's linguistic understanding of sentiment largely aligns with how customers numerically rate their experience. This validates BERT as a reliable tool for automatically assessing sentiment from text, which is vital for scaling feedback analysis.
By understanding how textual sentiment maps to star ratings, the business can prioritize. For instance, any review where BERT predicts '1 star' (even if the user gave a slightly higher rating) should be flagged for immediate attention, as the model detects strong negative language. This allows for a more nuanced and automated understanding of customer dissatisfaction beyond just the numerical rating.
When combined, this analysis allows the business to say, for example, 'Customers giving 2-star ratings often use language that BERT interprets as 1-star, focusing on 'long wait times' and 'cold food'.' This links the numerical star rating to the specific textual complaints identified by the NLP model, providing concrete areas for operational improvement.
Conclusion and Operational Steps
The analysis of customer reviews has revealed critical insights into the operational strengths and weaknesses of the McDonald's location. While there are segments of highly satisfied customers, a significant portion experiences issues related to service speed, order accuracy, and food quality, particularly at the drive-thru and during peak hours. The sentiment analysis highlights that even moderately rated reviews often contain strong negative language, indicating underlying dissatisfaction.
Based on these findings, the business should proceed with the following operational steps:
1.	Optimize Drive-Thru Operations
Implement real-time monitoring of drive-thru wait times and order accuracy. Review staffing levels during identified peak times ('morning', 'night', 'lunch') to ensure adequate personnel.
Reduce wait times and improve order accuracy to convert frequent 1-star reviews related to 'wait' and 'wrong order' into positive experiences.
2.	Enhance Food Quality Consistency
Conduct a focused audit on the preparation and holding procedures for frequently mentioned items like 'fries' and 'McChicken'. Implement stricter quality checks to ensure food is served hot and correctly prepared.
Address complaints about 'cold food' and 'incorrect preparation', directly impacting on customer satisfaction with product quality.
3.	Improve Staff Training and Empowerment
Provide additional training for front-line staff on handling complex orders, de-escalation techniques, and empowering them to resolve minor issues without immediate managerial intervention. Emphasize 'friendly' and 'efficient' service, as these are often cited in positive reviews.
Reduce mentions of 'manager' in negative contexts and improve the overall 'service' and 'customer' interaction scores, mitigating issues like 'rude staff' or 'unresolved problems'.
4.	Leverage Automated Feedback Analysis:
Integrate the BERT-based sentiment analysis model into a system for continuously monitoring incoming reviews. Prioritize reviews flagged by the model as '1 star' or '2 stars', even if the numerical rating is slightly higher, for immediate follow-up.
Develop a proactive customer service response system, allowing management to quickly identify and address emerging patterns of dissatisfaction before they escalate or negatively impact brand reputation more broadly.
By systematically addressing these operational areas, the McDonald's location can significantly improve customer experience, reduce negative feedback, and bolster its reputation.


