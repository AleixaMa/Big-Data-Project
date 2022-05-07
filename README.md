# Big-Data-Project
Extra credit assignment
Read Me

Our groups will all work on perm vis sonship data but with different focus. We have included three separate readme files each describing our respective part of the analytic (We think this will be more clear to follow than mixing our analytics together).

The purpose of my part of the analytics is to discover the relationship between economic index GNI (Gross national income) and per visa sponsorships.

I will work on cleaning the GNI dataset, and merging it with the cleaned PERM dataset (provided by Tanyue) using Hive. The analytics will be conducted on the merged dataset.

The majority of analytics is done in hive. Some data cleaning is performed before importing to Hive using map reduce. This follows the normal cleaning step in Hw 7, but the java code has been updated since hw7.

To run the analytics, follow the step-by-step solution provided below. You could also choose to skip the map-reduce cleaning step and directly use the cleaned dataset provided in the shared project folder under dataset directory: project/dataset/clean_gni &  project/dataset/clean_perm, load those data into hive tables and run the queries as shown in the query script within the analytic directory (All queries are listed in sequence and step is clearly marked). Coping and pasting each query in the same order as it appears in the query script should be sufficient for running the analytics in hive.


Detailed steps:

1.  Move the cleaned PERM dataset (cleaned and provided by Tanyue) to peel using scp.

scp /Users/mashuyang/Desktop/part-r-00000.csv sm8068@peel.hpc.nyu.edu:/home/sm8068

2. Move the raw original GNI dataset to peel using scp.

scp /Users/mashuyang/Desktop/GNI_dataset.csv sm8068@peel.hpc.nyu.edu:/home/sm8068

3. Move above two datasets from Peel to hdfs

hdfs dfs -put part-r-00000.csv project/dataset/perm_clean.csv
hdfs dfs -put GNI_dataset.csv project/dataset/GNI_dataset.csv

4. Go to the directory that contains clean.jar, and run it with GNI_dataset.csv as input, and project/clean_gni_output as output directory (delete the directory first if it already exists)

hadoop jar clean.jar Clean project/dataset/GNI_dataset.csv /user/sm8068/project/clean_gni_output

5. Move the output of map reduce job to project/dataset and rename it to gni_clean.csv

hdfs dfs -mv project/clean_gni_output/part-m-00000 project/dataset/gni_clean.csv

6. Now the cleaning step is finished. Login to hive, and the rest of analytics are all conducted using hive queries. The hive query script (with the name shuyang) in the analytic directory contains all the queries needed to run my part of the
 analytic from the very start to the very end. The queries are also arranged in the correct order. The queries are documented with comments and should be easy to follow. 

Note: you could skip step 1-5 and directly enters step 6 if you directly use the gni_clean.csv provided in project/dataset directory on my hdfs.

7. The results of the HiveQL analytics will be stored as hive tables in hive database

8. If somehow you don't have access to my project/dataset folder (this is unlikely since I definitely set the ACL, but just in case this happens), please contact me and let me know.
 



