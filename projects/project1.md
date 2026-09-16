#Project 1:
#Demographic Disparities in Young Adult Mental Health Care

##Problem Defenition:
###Question:  How does the gap between self-reported symptoms of (anxiety/depression) and actual mental health service utilization vary across race, sex and age demographic of young adults (18–34) in the United States? 

Early adulthood(age 18-34) represents a very critical transition for many in the United States. Pursuing higher education, joining the workforce, starting families and navigating independence usually coincide with increased rates of anxiety, depression and other mental health issues. While mental health awareness and support are expanding there still lies a divide between those experiencing mental health struggles and actually receiving treatment. This gap is particularly noticeable when examined through racial and gender inequalities, since stigma, systematic barriers and socioeconomic inequalities have created uneven access to health care. Identifying how these disparities vary across different demographics is necessary for healthcare systems, policymakers and mental health support to design targeted solutions to remove barriers and provide equitable mental health support for all young adults.

The aggregated nature of the CDC NHIS public API requires analyzing these demographic variables as independent (Age, Sex, and Race/Ethnicity separately).

##Data Description:
Data Source: CDC National Health Interview Survey (NHIS) API: 
https://data.cdc.gov/Mental-Health/National-Health-Interview-Survey-NHIS-Mental-Healt/d89q-62iu/about_data. The data comes from the CDC which is the government data base, it is relatively trust worthy but evidently like all data may have bias and underrepresented populations. The dataset contains 566 rows and 9 columns spanning many demographics such as age, sex, and race. Data collection assumes representative sampling across U.S. households however, self-reporting introduces underreporting risks and bias in marginalized or highly stigmatized demographics.
The gap between symptoms and treatment is what we are going to conceptualize. We will take self assessment of anxiety symptoms in the past year and depression symptoms in the past year and compare both these percentages to the percentage who saw a medical professional for treatment in the past year. My variables include age, I am choosing to look at the young adult group which represents early stages of adulting a very transitional period. This is in our data set as age 18-34. Sex is my second variable this is a demographic reflecting biological sex at birth which is in our data set as male or female. Race is my third variable this is your racial category that reflects lived experince and access to care. In our data set the categories are Black, Hispanic, Asian, White, AI/AN which is American Indian, NHOPI and multiracial. Self reported anxiety and self reported depression are two of the variables I am using to represent mental health issues. This is in our data as the percentages who self report high intensities of these feelings over the past year. Finally therapy utilization is those who interact with a mental health professional in any capacity to seek treatment. In our data set it is conceptualized as those seeing treatment in the past 12 months. 

##Context in how I operationalized: Treatment utilization encompasses all mental health services beyond just the symptoms, whereas symptom variables measure high-intensity anxiety and depression specifically. Consequently, treatment percentages naturally exceed isolated symptom metrics across most demographics.

##Data Cleaning and Preparation: 
In python I used pandas to filter and clean the API data set. This is because it contained many variables I did not need. 
It contains 566 rows of data, and 9 columns. I am unable to select age, race and gender all at once so when cleaning the data so I pulled these out as featured data to compare. I look at the age group 18-34 as one variable, race as a second and sex as the third. When I looked at race and sex it is not just the age group 18-34 since my data can not be viewed in that way. Rather I must look at the data as separate pieces. To clean the data I filtered the data to only use NHIS data and not the teen data. I had to convert the percentages into numeric floats to be able to use and compare. I filtered demographic types to focus on race and sex. Finally I isolated the three specific data set questions I was utilizing to examine my research question. I also filtered my data to look at the most recent data from 2024. These are all the steps I did to clean my data. I left in missing variables during cleaning to show where not enough data was collected. I decided this was important since my research question was focused on underrepresentation and systematic disparities. So rather then removing missing variables I left them in to see where we have gaps. 

#filters so we only have the NHIS data 

df_clean = data[data["Data_Source"] == "NHIS"].copy()

#makes the percent data all numeric 

df_clean["Percent"] = pd.to_numeric(df_clean["Percent"], errors="coerce")

#filtering for the two demographics I am interest in and the age group 

df_clean = df_clean[
    df_clean["Demographics_Type"].isin(["Age", "Sex", "RaceEthnicity"]) 
 
]

#selecting for only the variables I want to explore

clean_cols = [
    "Year",
    "Question",
    "Demographics_Type",
    "Demographics_Value",
    "Percent",
]

df_final = df_clean[clean_cols].reset_index(drop=True)

df_final.head()



##Visualizations 
All my visualizations show that my original hypothesis wasn’t represented. Treatment showed a higher percentage than self reported measures. This is due to treatment being utilized for much more than just high rates of depression and anxiety which I did not account for in my original research question. However I still gain results from my data. I am able to compare how race and sex influence treatment and self reported measures despite not being able to view the treatment gap itself. I also was unable to look at just the age group by itself so it became a separate variable I looked at in the heat map. To see how the specific age group of all races and sex compares to individual races and sex of all ages. 
<img width="1060" height="715" alt="Screenshot 2026-09-13 at 6 37 26 PM" src="https://github.com/user-attachments/assets/551c6cad-79cb-48ab-b14e-11e5c31911e3" />
My first visualization shows different racial groups and the percentage in treatment and reporting symptoms. Asian and Hispanic have the lowest rates whereas the white population comes in with the highest percentages. This shows how white have more access and less stigma regarding mental health and how disparities among both self report and treatment differ based on race. 

We have missing bars for American Indian and Native Hawaiian showing where populations did not have enough data which shows underrepresentation and gaps in our data set. I chose to keep the variables to show areas we could improve on. When looking at the data itself we see the disparity. It would be unlikely that specific racial demographics actually have that much lower rates of anxiety and depression more likely points to cultural stigma, diagnostic framing biases, or institutional reporting barriers.


<img width="884" height="540" alt="Screenshot 2026-09-13 at 6 40 24 PM" src="https://github.com/user-attachments/assets/3e2c2a36-2257-48b7-a30d-3db1cc3bf212" />
My second visualization shows sex instead of race. This shows how females report higher percentages in all three categories. However, the treatment gap between males and females is narrower than the symptom gap, pointing to potential male underreporting due to stigma and societal pressure surrounding mental health. 


<img width="744" height="481" alt="Screenshot 2026-09-13 at 6 42 13 PM" src="https://github.com/user-attachments/assets/80ef305b-5d44-4292-a911-6f9fdeeae79c" />
My third visualization shows a heat map comparing the percentages among all my variables. Placing age, sex, and race side by side demonstrates there is wide variation among demographic and mental health variables. We can see in all but the American Indian population treatment exceeds anxiety/depression symptoms. This reiterates that treatment is not solely used for these mental health conditions. Furthermore we can now see the age demographic we wanted to look at and see how this age population has higher rates of all categories, which reflects the transitional period of young adulthood being stressful. 

##Overall Correct and Incorrect Conclusions: 
The data shows that treatment goes far beyond the scope of just the two isolated variables anxiety and depression symptoms. It also shows the young adult population does see an increase in those reporting both symptoms and treatment reflecting how this is a huge adjustment period in ones life. 
Incorrect conclusions to draw would be that men have less mental health symptoms then female counterparts. What is more correct to assume is that societal pressure causes under reporting in self reporting data. Similarly it would be incorrect to assume Asians experince less mental health issues. This underrepresentation is also likely due to stigma and historical disparities. 

##Limitations, Ethics and Reflection: 
This project did not go the way I expected at all. I expected treatment to be lower than reported symptoms to highlight how disparities among sex and race intersect treatment opportunities. Although this is still a good research question my data did not necessarily reflect this. It showed how treatment for the most part exceeded anxiety/depression self reported measures. I had to adjust my reporting to reflect what the data actually shows, not force my original question and hypothesis. This was an important lesson to learn that the data will not always reflect what I want it to, but it is important to not lie and force your fidings. This is due to treatment being used for a combination of things and not solely just anxiety or depression. Similarly I was unable to just focus on young adults because the way the data was set up you could not select for age and race and gender, you could only select for one at a time. However in the heat map I could show age, gender and race side by side to show comparisons and interactions. Similarly the data had sex not gender so we could not include populations like intersex and nonbinary which would most likely provide interesting data. Another limitation is selfreported data and the basis that come with this. Cultural and gender stigmas lower symptom reporting among men and minorities, which we can see reflected in our data. Finally we had some empty variables that I left during data cleaning to show where my data was limited and racial groups were underrepresented due to not enough response data. 

In the future I would find a method or different data set to find a way to look at specific individuals with many demographics. So I could look at the targeted age group gender and sex all at the same time rather then separately. Similarly I would find a different way to operationalize symptoms that way we could see more of the treatment disparity to see where treatment is lacking in a more clear way. I think my biggest take away from this project is the important of finding the right data set. The findings I found are still super useful for disparities in mental health however, did not support my original research question to the fullest extent as we could not segment for all demographics at once, rather we looked at them independelty. 

#Code Transparency and Sources: 
[View Rendered Jupyter Notebook](https://Sarah123443321.github.io/data-science-portfolio/Data_Society_Project.html) 

Quinn, C. (2019, September 6). Transgender and non-binary students face “enormous” disparities in mental health problems, study finds. GBH. https://www.wgbh.org/news/local/2019-08-20/transgender-and-non-binary-students-face-enormous-disparities-in-mental-health-problems-study-finds 

Shi, P., Yang, A., Zhao, Q., Chen, Z., Ren, X., & Dai, Q. (2026, September 13). A hypothesis of gender differences in self-reporting symptom of depression: Implications to solve under-diagnosis and under-treatment of depression in males. Frontiers. https://www.frontiersin.org/journals/psychiatry/articles/10.3389/fpsyt.2021.589687/full 

Van Doren, N., Zhu, Y., Vázquez, M. M., Shah, J., Grammer, A. C., Fitzsimmons-Craft, E. E., Eisenberg, D., Wilfley, D. E., Taylor, C. B., & Newman, M. G. (2024, September 1). Racial and ethnic disparities in barriers to mental health treatment among U.S. college students. Psychiatric services (Washington, D.C.). https://pmc.ncbi.nlm.nih.gov/articles/PMC11537208/ 



Google Gemini (2026 version) was used to help troubleshoot code cleaning methods, and edit flaws in the visualizations.

Seaborn https://seaborn.pydata.org/index.html# was used as a refernce to make visualizations. 









