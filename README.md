# stackoverflow-nlp-sbert-classification

# Stack Overflow NLP Question Categorisation

This project looks at NLP-related questions posted on Stack Overflow and groups them into different categories based on what the user is asking.

The main idea was to use **Sentence-BERT (SBERT)** to understand the meaning of a question rather than relying only on matching keywords. The project uses SQL for data collection and Python for cleaning, analysis, visualisation and NLP modelling.

## Dataset

The data was collected from **Stack Exchange Data Explorer** using SQL. The final dataset contains **20,430 Stack Overflow questions** tagged with `nlp`.

The SQL query combines information from multiple Stack Exchange tables and collects:

* Post ID
* Post title
* Description
* Creation date
* Views
* Tags
* Accepted answer ID
* Accepted answer creation date
* Accepted answer body

Questions without an accepted answer were also retained so that they could still be included in the analysis.

## Data Cleaning and Exploration

Before analysing the data, I cleaned the text to make it easier to work with. This included:

* Removing HTML content using Beautiful Soup
* Removing punctuation and unnecessary symbols
* Converting text to lowercase
* Tokenising the text
* Removing English and custom stop words

I then explored the dataset to understand the type of content available before moving to categorisation.

Some of the analysis included:

* Posts with and without accepted answers
* Average and median response time
* Number of views
* Most frequently used tags
* Common words appearing in NLP-related questions

Out of the 20,430 questions, **8,509 had an accepted answer and 11,921 did not**.

An interesting result was the difference between the median and average time taken to receive an accepted answer. The median was around **4 hours and 9 minutes**, while the average was much higher because some questions took a very long time to receive an accepted answer.

## Question Categorisation

The main part of the project was categorising the Stack Overflow questions based on their meaning.

For the model input, I combined each question's **title and description**. I did not use the accepted answer because more than half of the questions did not have one.

The categories included areas such as:

* Implementation issues
* Conceptual understanding
* Model evaluation and optimisation
* Data preprocessing
* Feature extraction
* Tool or library recommendations
* Error-related questions
* Learning resources or advice

I used **Sentence-BERT** to generate sentence embeddings for both the questions and the category descriptions.

Cosine similarity was then calculated between each question and the available categories. The question was assigned to the category with the highest similarity score.

## Results

The largest category was **feature extraction-based questions**, followed by **tool or library recommendations** and **model evaluation/optimisation**.

The categorisation produced the following distribution:

| Category                                  | Number of Posts |
| ----------------------------------------- | --------------: |
| Feature extraction-based questions        |           7,916 |
| Tool or library recommendation            |           3,825 |
| Model evaluation optimisation             |           3,773 |
| Data preprocessing                        |           2,369 |
| Data loading / file handling              |           1,012 |
| Conceptual understanding                  |             773 |
| Implementation or error-related questions |             569 |
| Learning resources or advice              |             193 |

## Model Evaluation

I manually reviewed questions from the generated categories to check whether the assigned category made sense.

Most of the reviewed questions were placed in relevant categories, although I found cases where a question could reasonably belong to more than one category.

This highlighted one of the main limitations of the approach: the model assigns each question to only **one category**, even when the question may cover multiple topics.

A possible improvement would therefore be to use a **multi-label classification approach**, where one question can be assigned to more than one relevant category.

## Tools and Technologies

* Python
* SQL
* Sentence-BERT (SBERT)
* Sentence Transformers
* Beautiful Soup
* Regular Expressions
* Pandas
* NLP
* Cosine Similarity
* Data Visualisation

## Project Workflow

`SQL Data Extraction` → `Data Cleaning` → `Exploratory Analysis` → `Text Preparation` → `SBERT Embeddings` → `Cosine Similarity` → `Question Categorisation` → `Manual Evaluation`

## Why I Built This

Stack Overflow contains a large amount of useful technical knowledge, but finding relevant information can become difficult when similar problems are described in different ways.

This project was an attempt to organise NLP-related questions based on their semantic meaning. The broader idea is that this type of categorisation could be used as a starting point for building a domain-specific knowledge base where existing technical questions and solutions can be searched and organised more effectively.

## Future Improvements

There are several ways I would extend this project:

* Use multi-label classification for questions that belong to multiple categories
* Compare SBERT with other embedding or classification approaches
* Automate the evaluation process using a labelled validation dataset
* Improve category definitions and investigate overlapping categories
* Build a semantic search system on top of the generated embeddings

## Author

**Kavish Sharma**
Master of Data Science — The University of Adelaide
