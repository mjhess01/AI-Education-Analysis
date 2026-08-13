
# AI Impact Analysis

In this analysis, we are looking at the relationship between education, AI and the job industry for anyone who is curious about what our future with AI could look like.


## Run Locally

Clone the project

```bash
  git clone https://github.com/mjhess01/AI-Impact-Analysis
```

Go to the project directory

```bash
  cd AI_Impact_Analysis
```

Create and activate a new virtual environment in the folder

```bash
# windows
source venv/Scripts/activate
# mac / linux
source venv/bin/activate
```

Install dependencies

```bash
# windows
pip install -r requirements.txt
# mac / linux
pip3 install -r requirements.txt
```

Open the project

```bash
code .
```


## Questions and Findings

When I began this project, I had to identify my bias. I am not very trusting of AI, not because it is inherantly bad, but because people will often misuse it. I came at this projec from two angles: the professional side of AI use, and the educational side of AI use. 

When I looked at the dataset with the student information, the very first thing that drew my eyes was the effect AI had on GPA. I was prepared for it to impact negatively, but according to the charts below, I see that for the most part, the increase in GPA seems to far outnumber the cases where GPA decreased or stayed the same. 

<img width="636" height="658" alt="image" src="https://github.com/user-attachments/assets/cdd19a60-b9ef-4290-a6ab-ea4db45e72d7" />
<img width="636" height="658" alt="image" src="https://github.com/user-attachments/assets/777ca3c8-61c9-4ba7-8b53-9f02870a8ca9" />
<img width="636" height="658" alt="image" src="https://github.com/user-attachments/assets/8d28399a-d358-4e0f-83ee-596517727080" />

I chose three of the educational usage cases out of the five due to their difference in medium. I checked Essay Drafting, which I could easily see being impacted positively since that is something a student can use in the moment to boost the quality of their work. I expected Exam Prep to more negatively impact GPA, due to it being something you use initially and then perform the task without the direct use of AI in the moment, however just like in the other cases, there are more increases in GPA than there are decreases or unchanged GPAs combined.

I was also curious of which AI tools were typically used for what purpose. In the below visualization, I notice Gemini was used more than others in Brainstorming and Exam Prep and less than others in the Coding, Literature and Essay categories. This leads me to believe that it might be a better tool for more broad questions and tasks, such as "help me study this topic" rather than longer, more detailed review of documents.

<img width="1019" height="729" alt="image" src="https://github.com/user-attachments/assets/2cee11fe-85d5-485c-b5d0-3cb71d785ea2" />

Moving on to the professional look at AI use, my interest focused on what companies were gaining from this change and what employees were gaining (or losing) from this change. I wanted to use the years provided to look at changes in time across the first 5 years of this decade. I paired that with the rate of adoption, consumer trust, and revenue increase. From the line chart below, there was not an easily identifiable long term trend, though at the peak of adoption rate, we also had the peak of consumer trust, and the lowest increase in revenue. I found it a bit strange that consumer trust went up and revenue increase went down.

<img width="850" height="565" alt="image" src="https://github.com/user-attachments/assets/6e8fa0eb-8a68-416a-8b3a-b2bee82d2a38" />

Up next, I wanted to compare the revenue increase and adoption rate again, but this time with job loss. My initial thought was to see if the revenue increase and job loss increased at the same time, assuming that the revenue increase came from having to pay less people to work. I could also see the alternative, being that revenue increased to the number of job openings increased. However, there didn't seem to be a correlation at all between the three factors. 

<img width="850" height="547" alt="image" src="https://github.com/user-attachments/assets/0c386552-a325-478e-a313-fe4b38f3ff26" />

## Functions

```python
#perform an introductory check with any dataframes put into the argument

def intro_report(list_of_df):
    for df in list_of_df:
        print("Overview of Dataframes")
        print("\nFirst 5 Rows:")
        print(df.head())
        print("\nLast 5 Rows:")
        print(df.tail())
        print('\nNulls and Data Types:')
        print(df.info())
        print('\nRows by Columns')
        print (df.shape)

intro_report([student_life_df, content_df, jobs_df])
```

```python
#apply a single naming convention to all dataframes

def standardize(list_of_df):
    for df in list_of_df:
        df.columns = df.columns.str.lower().str.replace(" ", "_")

standardize([student_life_df, content_df, jobs_df])
```

```python
#create a dictionary map
domains_map = dict(zip(domains_df['domain_name'], domains_df['domain_id']))
#create a function for mapping foreign keys to dataframes before being made into tables
def fkmapping(df_name, col_name, col_name2, map_name):
    df_name[col_name] = df_name[col_name2].map(map_name)
    return df_name

#map the foreign key domain_id to student life matching on the majors 
fkmapping(student_life_df, 'domain_id', 'major', domains_map)
```
## Data Sources
| Author | Title / Link | Purpose |
|:--|:--|:--|
| **Akash Kumar Barnwal** | [`AI Impact on Job Sector`](https://www.kaggle.com/datasets/sumeakash/ai-impact-on-job-sector) | Salary before and post AI, job satisfaction and other details concerning jobs and industries. |
| **Atharva Soundankar** | [`Impact of AI on Digital Media (2020-2025)`](https://www.kaggle.com/datasets/atharvasoundankar/impact-of-ai-on-digital-media-2020-2025) | Job loss statistics, revenue increases, top AI tools used, focused on industries. |
| **Sohaib Malik** | [`AI and Student Life 2026`](https://www.kaggle.com/datasets/sohaibdevv/ai-and-student-life-2026-the-new-normal) | GPA baseline and post AI, student information and career confidence centered around college age students and their majors.|

## License

[MIT](https://choosealicense.com/licenses/mit/)

[Apache 2.0](https://choosealicense.com/licenses/apache-2.0/)

[CC0: Public Domain](https://creativecommons.org/publicdomain/zero/1.0/)

## Authors

- [@mjhess01](https://github.com/mjhess01)
