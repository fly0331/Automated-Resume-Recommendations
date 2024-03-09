# Automated-Resume-Recommendations

## PROJECT PURPOSE
In today's competitive job market, newcomers often feel lost when writing their first resume, unsure how to effectively showcase their experiences and skills. We aim to develop a text mining-based system to assist job seekers in writing resumes with a clearer direction.

This system analyzes the job title, job responsibilities, and past experiences entered by the user, and matches and provides the most relevant description examples from a database. This not only helps job seekers gain inspiration but also helps them understand the key skills and experiences required for specific positions. This project will provide valuable resources to job seekers, making the job search process smoother and effectively increasing their chances of finding ideal employment opportunities.

We have selected job categories closely related to information management (including Software Engineer, Project Manager, Information Technology, Data Analyst, etc.) as the targets for our end-of-term project.

## ABSTRACT
Our team designs an English resume content generator tailored for the information technology field to address the struggles Taiwanese students face when writing English resumes. The development process of this system can be divided into three stages:

1. Data Collection: Information technology-related English resume data is collected and organized through web scraping.

2. Preprocessing: Job titles and job descriptions are tokenized, normalized, and transformed into TF-IDF vectors, which are then stored in a database.

3. Implementation: In the first step, users input the desired job title as a query term. The system recommends the five most relevant job titles for the user to choose from. In the second step, based on the selected job title, the system generates a word cloud of commonly used words in that job title. Users are then prompted to input additional job content keywords based on the word cloud. Finally, the system generates five job content descriptions for users to reference when writing their English resumes.

### KEYWORDS 
Information Retrieval,
Content Generator
### CSS CONCEPTS 
* Information Systems
* Information Retrieval
* Query Processing

## LITERATURE REVIEW
Term Frequency-Inverse Document Frequency (TF-IDF) was initially proposed in the 1970s by researchers in the field of information retrieval. Originally used to improve the relevance assessment of search results, it has since been widely applied in various text-related applications such as document classification and topic modeling. Term Frequency (TF) measures the frequency of a term appearing in a document, while Inverse Document Frequency (IDF) measures the general importance of a term. The IDF of a specific term can be calculated by dividing the total number of documents by the number of documents containing that term, and then taking the logarithm of the quotient with 2 as the base. TF-IDF is a statistical method widely used in information retrieval and text mining. It is used to assess the importance of a term in a document collection or database. The TF-IDF value increases with the frequency of the term appearing but decreases with the number of documents containing the term in the corpus, helping to filter out common terms and retain important ones.

## DATA COLLECTION AND DATA CLEANING
We scraped resumes related to the information technology industry from Live Career, totaling 1,391 resumes. Through manual screening, we removed occupations unrelated to the information technology industry (e.g., Truck Driver, Chef, etc.) and merged similar job titles (e.g., Information Technology Manager and Information Technology Director were merged into Information Technology Manager). We also normalized job titles (e.g., Software Engineering was changed to Software Engineer). After these preprocessing steps, the database consisted of 230 unique job titles and 10,337 job content descriptions.

Example of data:
* Job Title: Software Engineer
* Job Content Description: Responsible for developing and maintaining software applications, debugging and troubleshooting code, collaborating with cross-functional teams, etc.
  
![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig1.png)

![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig2.png)

## DATA PREPROCESSING AND DATA TRANSFORMATION
Before using the user query, we preprocess the job titles and job content descriptions and save them in the form of TF-IDF vectors in the database. Below are the detailed steps of this preprocessing stage:

a. Keep only English text content.
b. Replace "IT" in the content description with "Information Technology" to correspond to the TF-IDF vector space.
c. Convert all content to lowercase English.
d. Remove leading and trailing whitespaces.
e. Remove stopwords.
f. Replace occurrences of more than two consecutive whitespaces with a single whitespace.
g. Apply Porter's Algorithm for stemming.

After completing the above preprocessing steps, compute the TF-IDF vectors for job titles and job content descriptions and save them in two tables for subsequent query usage.

Example of tables:
Jobtitle_tfidf.csv: Contains the TF-IDF values of terms appearing in all job titles within each job title (each job title is considered a document).

![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig3.png)

Jobline_tfidf.csv: Contains the TF-IDF values of terms appearing in all job content descriptions, where each job content description is treated as a document.

![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig4.png)

## PROJECT IMPLEMENTATION AND SYSTEM OUTCOMES
Our retrieval process can be broadly divided into five steps.

1. First Step: Prompt the user to input the desired job title as the system's query term.
(As shown in Figure 5)

![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig5.png)

3. Second Step: The system preprocesses the user-entered query term (e.g., Cloud Engineer) using the same preprocessing steps as described for job titles and job descriptions. Subsequently, it calculates the total TF-IDF score for each job title's query term. Then, it returns the top five job titles with the highest TF-IDF scores to provide users with options.
(As shown in Figure 6)

![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig6.png)

5. Third Step: After the user selects the most desired relevant job title (e.g., 5 Cloud Engineer), the system generates a word cloud. The word cloud's content is based on the most frequently occurring terms in the job descriptions associated with the user-selected job title.
(As shown in Figure 7)

![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig7.png)

7. Fourth Step: Users can refer to the word cloud generated by the system to add additional query terms (e.g., Python, Container) for the system to search for job descriptions that better meet their needs.
(As shown in Figure 7)

8. Fifth Step: The system will combine the selected relevant job titles and the query terms added by the user to perform TF-IDF ranking, listing the top five job descriptions with the highest TF-IDF scores for the user's reference.
(As shown in Figure 8)

![image](https://github.com/fly0331/Automated-Resume-Recommendations/blob/main/image/fig8.png)

## CONCLUSIONS, LIMITATIONS
The English resume generator designed by our team is built upon TF-IDF. When we pre-calculate the TF-IDF values, the system executes very quickly. However, one drawback is that it requires significant memory space for storage. In the future, if our English resume generator needs to cover professions beyond information technology, it will inevitably require even more storage space, posing a challenge for expanding the system. Additionally, in this project, we only used TF-IDF sorting to rank resume content. In the future, we can explore other techniques learned in class (such as Clustering) and other technologies in the field of text mining (such as Word2Vec) to enhance our English resume recommendation system.




































