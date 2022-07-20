# Project name: Cyclistic-Google-Project

# This R environment comes with many helpful analytics packages installed
# It is defined by the kaggle/rstats Docker image: https://github.com/kaggle/docker-rstats
# For example, here's a helpful package to load

library(tidyverse) # metapackage of all tidyverse packages

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

list.files(path = "../input")

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

✔ ggplot2 3.3.5     ✔ purrr   0.3.4
✔ tibble  3.1.6     ✔ dplyr   1.0.8
✔ tidyr   1.2.0     ✔ stringr 1.4.0
✔ readr   2.1.2     ✔ forcats 0.5.1

── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()

'cyclistic-data''cyclisticdata2'
Google capstone project
Started my google data analytics course few months ago with the aim of acquiring the necessary skills to become a data analyst. I have been able to successfully completed 8 courses of the course in which has helped me gained the necessary skills. In the course, we were taken through the processes involved in analysis starting from the ask phase to the act phase. Also learnt the use of tools like spreadsheet, sql, tableau and R. To round up the course, we were required to do a case study to build a portfolio, and below is mine. In this case study, I worked as a junior data analyst who joined the team six months ago and have been busy learning about Cyclistic’s mission and business goals — as well as how I can help Cyclistic achieve their goal.

Introduction
Cyclistic is a bike-share company. In 2016, they launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members. Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers. Director of marketing, Moreno believes that maximizing the number of annual members will be key to future growth. The manager has set a clear goal of designing marketing strategies aimed at converting casual riders into annual members. To achieve this, my team and I (the marketing analyst team) need to understand how casual riders and annual members use Cyclistic bikes differently, in order to design a new marketing strategy to convert casual riders into annual members. The interest lies in analyzing the Cyclistic historical bike trip data to identify trends.

PHASE 1 – ASK
Identifying the business task The problem we are trying to solve here is identifying the trends and behavior of the different customer segment of the Cyclistic bike company to enable us come up with a marketing strategy that can convert the casual members into annual members in order to increase growth for the company.

Considering key stakeholders I will be working closely with some of the key stakeholders which include: Lily Moreno: The director of marketing and my manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels. The marketing analytics team: A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy. *The executive team: The notoriously detail-oriented executive team that will decide whether to approve the recommended marketing program.

PHASE 2: PREPARE
The data was located in Cyclistic’s database and stored as zipped CSV files. It was made available by Motivate International Inc. under this license. The data was collected by Cyclistic company itself, thereby it’s reliable for the questions that needs to be solved.

PHASE 3: PROCESS
I downloaded the previous 12 months data as zipped files. I extracted the different CSV files into a folder and used RStudio to carry out data preparation and exploration. I decided to use this tool for the analysis because of its ability to handle large dataset. The steps taken will be listen below.

To begin, I had to install and load some packages that would be used in the analysis. The packages are Tidyverse to help wrangle data, readr for loading the datasets, ggplot2 for data visualization, lubridate package for working with dates, skimr and janitor for data manipulation.

library(tidyverse)

library(readr)
library(ggplot2)


library(skimr)

library(janitor)

library(stringr)
library(lubridate)
Attaching package: ‘janitor’


The following objects are masked from ‘package:stats’:

    chisq.test, fisher.test



Attaching package: ‘lubridate’


The following objects are masked from ‘package:base’:

    date, intersect, setdiff, union


library(readr)
Step 1: Collecting data
It's time to load our dataset into dataframes using the read.csv function

df_apr_2021 <- read_csv('../input/cyclistic-data/202104-divvy-tripdata.csv')
df_may_2021 <- read.csv('../input/cyclistic-data/202105-divvy-tripdata.csv')
df_jun_2021 <- read_csv('../input/cyclistic-data/202106-divvy-tripdata.csv')
df_jul_2021 <- read.csv('../input/cyclistic-data/202107-divvy-tripdata.csv')
df_aug_2021 <- read_csv('../input/cyclistic-data/202108-divvy-tripdata.csv')
df_sep_2021 <- read.csv('../input/cyclistic-data/202109-divvy-tripdata.csv')
df_oct_2021 <- read_csv('../input/cyclistic-data/202110-divvy-tripdata.csv')
df_nov_2021 <- read.csv('../input/cyclistic-data/202111-divvy-tripdata.csv')
df_dec_2021 <- read_csv('../input/cyclistic-data/202112-divvy-tripdata.csv')
df_jan_2022 <- read.csv('../input/cyclistic-data/202201-divvy-tripdata.csv')
df_feb_2022 <- read_csv('../input/cyclisticdata2/202202-divvy-tripdata.csv')
df_mar_2022 <- read.csv('../input/cyclisticdata2/202203-divvy-tripdata.csv')
Rows: 337230 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
Rows: 729595 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
Rows: 804352 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
Rows: 631226 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
Rows: 247540 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
Rows: 115609 Columns: 13
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
dbl  (4): start_lat, start_lng, end_lat, end_lng
dttm (2): started_at, ended_at

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
STEP 2: WRANGLE DATA AND COMBINE INTO A SINGLE FILE
Firstly, i had to check out my dataset to have a glimpse of it by comparing their column names and column type before combining together.

glimpse(df_apr_2021)
glimpse(df_may_2021)
glimpse(df_jun_2021)
glimpse(df_jul_2021)
glimpse(df_aug_2021)
glimpse(df_sep_2021)
glimpse(df_oct_2021)
glimpse(df_nov_2021)
glimpse(df_dec_2021)
glimpse(df_jan_2022)
glimpse(df_feb_2022)
glimpse(df_mar_2022)
Rows: 337,230
Columns: 13
$ ride_id            <chr> "6C992BD37A98A63F", "1E0145613A209000", "E498E15508…
$ rideable_type      <chr> "classic_bike", "docked_bike", "docked_bike", "clas…
$ started_at         <dttm> 2021-04-12 18:25:36, 2021-04-27 17:27:11, 2021-04-…
$ ended_at           <dttm> 2021-04-12 18:56:55, 2021-04-27 18:31:29, 2021-04-…
$ start_station_name <chr> "State St & Pearson St", "Dorchester Ave & 49th St"…
$ start_station_id   <chr> "TA1307000061", "KA1503000069", "20121", "TA1305000…
$ end_station_name   <chr> "Southport Ave & Waveland Ave", "Dorchester Ave & 4…
$ end_station_id     <chr> "13235", "KA1503000069", "20121", "13235", "20121",…
$ start_lat          <dbl> 41.89745, 41.80577, 41.74149, 41.90312, 41.74149, 4…
$ start_lng          <dbl> -87.62872, -87.59246, -87.65841, -87.67394, -87.658…
$ end_lat            <dbl> 41.94815, 41.80577, 41.74149, 41.94815, 41.74149, 4…
$ end_lng            <dbl> -87.66394, -87.59246, -87.65841, -87.66394, -87.658…
$ member_casual      <chr> "member", "casual", "casual", "member", "casual", "…
Rows: 531,633
Columns: 13
$ ride_id            <chr> "C809ED75D6160B2A", "DD59FDCE0ACACAF3", "0AB83CB88C…
$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", …
$ started_at         <chr> "2021-05-30 11:58:15", "2021-05-30 11:29:14", "2021…
$ ended_at           <chr> "2021-05-30 12:10:39", "2021-05-30 12:14:09", "2021…
$ start_station_name <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ start_station_id   <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ end_station_name   <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ end_station_id     <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ start_lat          <dbl> 41.90000, 41.88000, 41.92000, 41.92000, 41.94000, 4…
$ start_lng          <dbl> -87.63000, -87.62000, -87.70000, -87.70000, -87.690…
$ end_lat            <dbl> 41.89000, 41.79000, 41.92000, 41.94000, 41.94000, 4…
$ end_lng            <dbl> -87.61000, -87.58000, -87.70000, -87.69000, -87.700…
$ member_casual      <chr> "casual", "casual", "casual", "casual", "casual", "…
Rows: 729,595
Columns: 13
$ ride_id            <chr> "99FEC93BA843FB20", "06048DCFC8520CAF", "9598066F68…
$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", …
$ started_at         <dttm> 2021-06-13 14:31:28, 2021-06-04 11:18:02, 2021-06-…
$ ended_at           <dttm> 2021-06-13 14:34:11, 2021-06-04 11:24:19, 2021-06-…
$ start_station_name <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
$ start_station_id   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
$ end_station_name   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, "Michigan Ave &…
$ end_station_id     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, "13042", NA, NA…
$ start_lat          <dbl> 41.80, 41.79, 41.80, 41.78, 41.80, 41.78, 41.79, 41…
$ start_lng          <dbl> -87.59, -87.59, -87.60, -87.58, -87.59, -87.58, -87…
$ end_lat            <dbl> 41.80000, 41.80000, 41.79000, 41.80000, 41.79000, 4…
$ end_lng            <dbl> -87.6000, -87.6000, -87.5900, -87.6000, -87.5900, -…
$ member_casual      <chr> "member", "member", "member", "member", "member", "…
Rows: 822,410
Columns: 13
$ ride_id            <chr> "0A1B623926EF4E16", "B2D5583A5A5E76EE", "6F264597DD…
$ rideable_type      <chr> "docked_bike", "classic_bike", "classic_bike", "cla…
$ started_at         <chr> "2021-07-02 14:44:36", "2021-07-07 16:57:42", "2021…
$ ended_at           <chr> "2021-07-02 15:19:58", "2021-07-07 17:16:09", "2021…
$ start_station_name <chr> "Michigan Ave & Washington St", "California Ave & C…
$ start_station_id   <chr> "13001", "17660", "SL-012", "17660", "17660", "1766…
$ end_station_name   <chr> "Halsted St & North Branch St", "Wood St & Hubbard …
$ end_station_id     <chr> "KA1504000117", "13432", "KA1503000044", "13196", "…
$ start_lat          <dbl> 41.88398, 41.90036, 41.86038, 41.90036, 41.90035, 4…
$ start_lng          <dbl> -87.62468, -87.69670, -87.62581, -87.69670, -87.696…
$ end_lat            <dbl> 41.89937, 41.88990, 41.89017, 41.89456, 41.88659, 4…
$ end_lng            <dbl> -87.64848, -87.67147, -87.62619, -87.65345, -87.658…
$ member_casual      <chr> "casual", "casual", "member", "member", "casual", "…
Rows: 804,352
Columns: 13
$ ride_id            <chr> "99103BB87CC6C1BB", "EAFCCCFB0A3FC5A1", "9EF4F46C57…
$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", …
$ started_at         <dttm> 2021-08-10 17:15:49, 2021-08-10 17:23:14, 2021-08-…
$ ended_at           <dttm> 2021-08-10 17:22:44, 2021-08-10 17:39:24, 2021-08-…
$ start_station_name <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
$ start_station_id   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
$ end_station_name   <chr> NA, NA, NA, NA, NA, NA, NA, "Clark St & Grace St", …
$ end_station_id     <chr> NA, NA, NA, NA, NA, NA, NA, "TA1307000127", NA, NA,…
$ start_lat          <dbl> 41.77000, 41.77000, 41.95000, 41.97000, 41.79000, 4…
$ start_lng          <dbl> -87.68000, -87.68000, -87.65000, -87.67000, -87.600…
$ end_lat            <dbl> 41.77000, 41.77000, 41.97000, 41.95000, 41.77000, 4…
$ end_lng            <dbl> -87.68000, -87.63000, -87.66000, -87.65000, -87.620…
$ member_casual      <chr> "member", "member", "member", "member", "member", "…
Rows: 756,147
Columns: 13
$ ride_id            <chr> "9DC7B962304CBFD8", "F930E2C6872D6B32", "6EF7213790…
$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", …
$ started_at         <chr> "2021-09-28 16:07:10", "2021-09-28 14:24:51", "2021…
$ ended_at           <chr> "2021-09-28 16:09:54", "2021-09-28 14:40:05", "2021…
$ start_station_name <chr> "", "", "", "", "", "", "", "", "", "", "Clark St &…
$ start_station_id   <chr> "", "", "", "", "", "", "", "", "", "", "TA13070001…
$ end_station_name   <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ end_station_id     <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ start_lat          <dbl> 41.89000, 41.94000, 41.81000, 41.80000, 41.88000, 4…
$ start_lng          <dbl> -87.68000, -87.64000, -87.72000, -87.72000, -87.740…
$ end_lat            <dbl> 41.89, 41.98, 41.80, 41.81, 41.88, 41.88, 41.74, 41…
$ end_lng            <dbl> -87.67, -87.67, -87.72, -87.72, -87.71, -87.74, -87…
$ member_casual      <chr> "casual", "casual", "casual", "casual", "casual", "…
Rows: 631,226
Columns: 13
$ ride_id            <chr> "620BC6107255BF4C", "4471C70731AB2E45", "26CA69D43D…
$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", …
$ started_at         <dttm> 2021-10-22 12:46:42, 2021-10-21 09:12:37, 2021-10-…
$ ended_at           <dttm> 2021-10-22 12:49:50, 2021-10-21 09:14:14, 2021-10-…
$ start_station_name <chr> "Kingsbury St & Kinzie St", NA, NA, NA, NA, NA, NA,…
$ start_station_id   <chr> "KA1503000043", NA, NA, NA, NA, NA, NA, NA, NA, NA,…
$ end_station_name   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
$ end_station_id     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
$ start_lat          <dbl> 41.88919, 41.93000, 41.92000, 41.92000, 41.89000, 4…
$ start_lng          <dbl> -87.63850, -87.70000, -87.70000, -87.69000, -87.710…
$ end_lat            <dbl> 41.89000, 41.93000, 41.94000, 41.92000, 41.89000, 4…
$ end_lng            <dbl> -87.63000, -87.71000, -87.72000, -87.69000, -87.690…
$ member_casual      <chr> "member", "member", "member", "member", "member", "…
Rows: 359,978
Columns: 13
$ ride_id            <chr> "7C00A93E10556E47", "90854840DFD508BA", "0A7D10CDD1…
$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", …
$ started_at         <chr> "2021-11-27 13:27:38", "2021-11-27 13:38:25", "2021…
$ ended_at           <chr> "2021-11-27 13:46:38", "2021-11-27 13:56:10", "2021…
$ start_station_name <chr> "", "", "", "", "", "Michigan Ave & Oak St", "", ""…
$ start_station_id   <chr> "", "", "", "", "", "13042", "", "", "", "", "", ""…
$ end_station_name   <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ end_station_id     <chr> "", "", "", "", "", "", "", "", "", "", "", "", "",…
$ start_lat          <dbl> 41.93000, 41.96000, 41.96000, 41.94000, 41.90000, 4…
$ start_lng          <dbl> -87.72000, -87.70000, -87.70000, -87.79000, -87.630…
$ end_lat            <dbl> 41.96, 41.92, 41.96, 41.93, 41.88, 41.90, 41.80, 41…
$ end_lng            <dbl> -87.73, -87.70, -87.70, -87.79, -87.62, -87.63, -87…
$ member_casual      <chr> "casual", "casual", "casual", "casual", "casual", "…
Rows: 247,540
Columns: 13
$ ride_id            <chr> "46F8167220E4431F", "73A77762838B32FD", "4CF4245205…
$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", …
$ started_at         <dttm> 2021-12-07 15:06:07, 2021-12-11 03:43:29, 2021-12-…
$ ended_at           <dttm> 2021-12-07 15:13:42, 2021-12-11 04:10:23, 2021-12-…
$ start_station_name <chr> "Laflin St & Cullerton St", "LaSalle Dr & Huron St"…
$ start_station_id   <chr> "13307", "KP1705001026", "KA1504000117", "KA1504000…
$ end_station_name   <chr> "Morgan St & Polk St", "Clarendon Ave & Leland Ave"…
$ end_station_id     <chr> "TA1307000130", "TA1307000119", "13137", "KP1705001…
$ start_lat          <dbl> 41.85483, 41.89441, 41.89936, 41.89939, 41.89558, 4…
$ start_lng          <dbl> -87.66366, -87.63233, -87.64852, -87.64854, -87.682…
$ end_lat            <dbl> 41.87197, 41.96797, 41.93758, 41.89488, 41.93125, 4…
$ end_lng            <dbl> -87.65097, -87.65000, -87.64410, -87.63233, -87.644…
$ member_casual      <chr> "member", "casual", "member", "member", "member", "…
Rows: 103,770
Columns: 13
$ ride_id            <chr> "C2F7DD78E82EC875", "A6CF8980A652D272", "BD0F91DFF7…
$ rideable_type      <chr> "electric_bike", "electric_bike", "classic_bike", "…
$ started_at         <chr> "2022-01-13 11:59:47", "2022-01-10 08:41:56", "2022…
$ ended_at           <chr> "2022-01-13 12:02:44", "2022-01-10 08:46:17", "2022…
$ start_station_name <chr> "Glenwood Ave & Touhy Ave", "Glenwood Ave & Touhy A…
$ start_station_id   <chr> "525", "525", "TA1306000016", "KA1504000151", "TA13…
$ end_station_name   <chr> "Clark St & Touhy Ave", "Clark St & Touhy Ave", "Gr…
$ end_station_id     <chr> "RP-007", "RP-007", "TA1307000001", "TA1309000021",…
$ start_lat          <dbl> 42.01280, 42.01276, 41.92560, 41.98359, 41.87785, 4…
$ start_lng          <dbl> -87.66591, -87.66597, -87.65371, -87.66915, -87.624…
$ end_lat            <dbl> 42.01256, 42.01256, 41.92533, 41.96151, 41.88462, 4…
$ end_lng            <dbl> -87.67437, -87.67437, -87.66580, -87.67139, -87.627…
$ member_casual      <chr> "casual", "casual", "member", "casual", "member", "…
Rows: 115,609
Columns: 13
$ ride_id            <chr> "E1E065E7ED285C02", "1602DCDC5B30FFE3", "BE7DD2AF4B…
$ rideable_type      <chr> "classic_bike", "classic_bike", "classic_bike", "cl…
$ started_at         <dttm> 2022-02-19 18:08:41, 2022-02-20 17:41:30, 2022-02-…
$ ended_at           <dttm> 2022-02-19 18:23:56, 2022-02-20 17:45:56, 2022-02-…
$ start_station_name <chr> "State St & Randolph St", "Halsted St & Wrightwood …
$ start_station_id   <chr> "TA1305000029", "TA1309000061", "TA1305000029", "13…
$ end_station_name   <chr> "Clark St & Lincoln Ave", "Southport Ave & Wrightwo…
$ end_station_id     <chr> "13179", "TA1307000113", "13011", "13323", "TA13070…
$ start_lat          <dbl> 41.88462, 41.92914, 41.88462, 41.94815, 41.88462, 4…
$ start_lng          <dbl> -87.62783, -87.64908, -87.62783, -87.66394, -87.627…
$ end_lat            <dbl> 41.91569, 41.92877, 41.87926, 41.95283, 41.88584, 4…
$ end_lng            <dbl> -87.63460, -87.66391, -87.63990, -87.64999, -87.635…
$ member_casual      <chr> "member", "member", "member", "member", "member", "…
Rows: 284,042
Columns: 13
$ ride_id            <chr> "47EC0A7F82E65D52", "8494861979B0F477", "EFE527AF80…
$ rideable_type      <chr> "classic_bike", "electric_bike", "classic_bike", "c…
$ started_at         <chr> "2022-03-21 13:45:01", "2022-03-16 09:37:16", "2022…
$ ended_at           <chr> "2022-03-21 13:51:18", "2022-03-16 09:43:34", "2022…
$ start_station_name <chr> "Wabash Ave & Wacker Pl", "Michigan Ave & Oak St", …
$ start_station_id   <chr> "TA1307000131", "13042", "13109", "TA1307000131", "…
$ end_station_name   <chr> "Kingsbury St & Kinzie St", "Orleans St & Chestnut …
$ end_station_id     <chr> "KA1503000043", "620", "15578", "TA1305000025", "13…
$ start_lat          <dbl> 41.88688, 41.90100, 41.97835, 41.88688, 41.91172, 4…
$ start_lng          <dbl> -87.62603, -87.62375, -87.65975, -87.62603, -87.626…
$ end_lat            <dbl> 41.88918, 41.89820, 41.98404, 41.87771, 41.87794, 4…
$ end_lng            <dbl> -87.63851, -87.63754, -87.66027, -87.63532, -87.662…
$ member_casual      <chr> "member", "member", "member", "member", "member", "…
From the output above, it is seen that some of the dataframe have their columns (started_at and ended_at) formatted as chr instead of datetime. So I will have to convert the chr to datetime datatypes using as_datetime() function to maintain consistency

df_may_2021 <- mutate(df_may_2021, started_at = 
                            as_datetime(started_at),
                            ended_at = as_datetime(ended_at))
df_jul_2021 <- mutate(df_jul_2021, started_at = 
                        as_datetime(started_at),
                      ended_at = as_datetime(ended_at))
df_sep_2021 <- mutate(df_sep_2021, started_at = 
                        as_datetime(started_at),
                      ended_at = as_datetime(ended_at))
df_nov_2021 <- mutate(df_nov_2021, started_at = 
                        as_datetime(started_at),
                      ended_at = as_datetime(ended_at))
df_jan_2022 <- mutate(df_jan_2022, started_at = 
                        as_datetime(started_at),
                      ended_at = as_datetime(ended_at))
df_mar_2022 <- mutate(df_mar_2022, started_at = 
                        as_datetime(started_at),
                      ended_at = as_datetime(ended_at))
After having a glimpse of each dataframe and confirming they are all consistent, now i merge all together using the bind_rows function.
all_ride <- bind_rows(df_apr_2021, df_may_2021, df_jun_2021,
                        df_jul_2021, df_aug_2021, df_sep_2021,
                        df_oct_2021, df_nov_2021, df_dec_2021,
                        df_jan_2022, df_feb_2022, df_mar_2022)
STEP 3: CLEANING UP AND ADDING DATA TO PREPARE FOR ANALYSIS
Inspecting the new table that has been created by using the following functions

colnames() to check for the list of column names.
nrow() to check how many rows are in the data frame.
dim() to check for the dimensions of the data frame.
head() to see the first 6 rows of data frame. Also tail()
str() to see list of columns and data types (numeric, character, etc)
summary() to view the statistical summary of data. Mainly for numerics
colnames(all_ride)
nrow(all_ride)
dim(all_ride)
head(all_ride)
str(all_ride)
summary(all_ride)
'ride_id''rideable_type''started_at''ended_at''start_station_name''start_station_id''end_station_name''end_station_id''start_lat''start_lng''end_lat''end_lng''member_casual'
5723532
572353213
A tibble: 6 × 13
ride_id	rideable_type	started_at	ended_at	start_station_name	start_station_id	end_station_name	end_station_id	start_lat	start_lng	end_lat	end_lng	member_casual
<chr>	<chr>	<dttm>	<dttm>	<chr>	<chr>	<chr>	<chr>	<dbl>	<dbl>	<dbl>	<dbl>	<chr>
6C992BD37A98A63F	classic_bike	2021-04-12 18:25:36	2021-04-12 18:56:55	State St & Pearson St   	TA1307000061	Southport Ave & Waveland Ave	13235       	41.89745	-87.62872	41.94815	-87.66394	member
1E0145613A209000	docked_bike	2021-04-27 17:27:11	2021-04-27 18:31:29	Dorchester Ave & 49th St	KA1503000069	Dorchester Ave & 49th St    	KA1503000069	41.80577	-87.59246	41.80577	-87.59246	casual
E498E15508A80BAD	docked_bike	2021-04-03 12:42:45	2021-04-07 11:40:24	Loomis Blvd & 84th St   	20121       	Loomis Blvd & 84th St       	20121       	41.74149	-87.65841	41.74149	-87.65841	casual
1887262AD101C604	classic_bike	2021-04-17 09:17:42	2021-04-17 09:42:48	Honore St & Division St	TA1305000034	Southport Ave & Waveland Ave	13235       	41.90312	-87.67394	41.94815	-87.66394	member
C123548CAB2A32A5	docked_bike	2021-04-03 12:42:25	2021-04-03 14:13:42	Loomis Blvd & 84th St   	20121       	Loomis Blvd & 84th St       	20121       	41.74149	-87.65841	41.74149	-87.65841	casual
097E76F3651B1AC1	classic_bike	2021-04-25 18:43:18	2021-04-25 18:43:59	Clinton St & Polk St    	15542       	Clinton St & Polk St        	15542       	41.87147	-87.64095	41.87147	-87.64095	casual
spec_tbl_df [5,723,532 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ ride_id           : chr [1:5723532] "6C992BD37A98A63F" "1E0145613A209000" "E498E15508A80BAD" "1887262AD101C604" ...
 $ rideable_type     : chr [1:5723532] "classic_bike" "docked_bike" "docked_bike" "classic_bike" ...
 $ started_at        : POSIXct[1:5723532], format: "2021-04-12 18:25:36" "2021-04-27 17:27:11" ...
 $ ended_at          : POSIXct[1:5723532], format: "2021-04-12 18:56:55" "2021-04-27 18:31:29" ...
 $ start_station_name: chr [1:5723532] "State St & Pearson St" "Dorchester Ave & 49th St" "Loomis Blvd & 84th St" "Honore St & Division St" ...
 $ start_station_id  : chr [1:5723532] "TA1307000061" "KA1503000069" "20121" "TA1305000034" ...
 $ end_station_name  : chr [1:5723532] "Southport Ave & Waveland Ave" "Dorchester Ave & 49th St" "Loomis Blvd & 84th St" "Southport Ave & Waveland Ave" ...
 $ end_station_id    : chr [1:5723532] "13235" "KA1503000069" "20121" "13235" ...
 $ start_lat         : num [1:5723532] 41.9 41.8 41.7 41.9 41.7 ...
 $ start_lng         : num [1:5723532] -87.6 -87.6 -87.7 -87.7 -87.7 ...
 $ end_lat           : num [1:5723532] 41.9 41.8 41.7 41.9 41.7 ...
 $ end_lng           : num [1:5723532] -87.7 -87.6 -87.7 -87.7 -87.7 ...
 $ member_casual     : chr [1:5723532] "member" "casual" "casual" "member" ...
 - attr(*, "spec")=
  .. cols(
  ..   ride_id = col_character(),
  ..   rideable_type = col_character(),
  ..   started_at = col_datetime(format = ""),
  ..   ended_at = col_datetime(format = ""),
  ..   start_station_name = col_character(),
  ..   start_station_id = col_character(),
  ..   end_station_name = col_character(),
  ..   end_station_id = col_character(),
  ..   start_lat = col_double(),
  ..   start_lng = col_double(),
  ..   end_lat = col_double(),
  ..   end_lng = col_double(),
  ..   member_casual = col_character()
  .. )
 - attr(*, "problems")=<externalptr> 
   ride_id          rideable_type        started_at                 
 Length:5723532     Length:5723532     Min.   :2021-04-01 00:03:18  
 Class :character   Class :character   1st Qu.:2021-06-22 15:20:26  
 Mode  :character   Mode  :character   Median :2021-08-17 18:25:49  
                                       Mean   :2021-08-26 22:25:18  
                                       3rd Qu.:2021-10-14 19:48:10  
                                       Max.   :2022-03-31 23:59:47  
                                                                    
    ended_at                   start_station_name start_station_id  
 Min.   :2021-04-01 00:14:29   Length:5723532     Length:5723532    
 1st Qu.:2021-06-22 15:47:37   Class :character   Class :character  
 Median :2021-08-17 18:44:32   Mode  :character   Mode  :character  
 Mean   :2021-08-26 22:46:50                                        
 3rd Qu.:2021-10-14 20:03:28                                        
 Max.   :2022-04-01 22:10:12                                        
                                                                    
 end_station_name   end_station_id       start_lat       start_lng     
 Length:5723532     Length:5723532     Min.   :41.64   Min.   :-87.84  
 Class :character   Class :character   1st Qu.:41.88   1st Qu.:-87.66  
 Mode  :character   Mode  :character   Median :41.90   Median :-87.64  
                                       Mean   :41.90   Mean   :-87.65  
                                       3rd Qu.:41.93   3rd Qu.:-87.63  
                                       Max.   :45.64   Max.   :-73.80  
                                                                       
    end_lat         end_lng       member_casual     
 Min.   :41.39   Min.   :-88.97   Length:5723532    
 1st Qu.:41.88   1st Qu.:-87.66   Class :character  
 Median :41.90   Median :-87.64   Mode  :character  
 Mean   :41.90   Mean   :-87.65                     
 3rd Qu.:41.93   3rd Qu.:-87.63                     
 Max.   :42.17   Max.   :-87.49                     
 NA's   :4716    NA's   :4716                       
From above, it can be seen that all_ride contains 5,723,532 rows and 13 columns.

Extracting columns that list the date, month, day, and year of each ride from column started_at. This will allow us to aggregate ride data for each month, day, or year.

all_ride$date <- as.Date(all_ride$started_at)
all_ride$month <- format(as.Date(all_ride$date), "%m")
all_ride$day <- format(as.Date(all_ride$date), "%d")
all_ride$year <- format(as.Date(all_ride$date), "%Y")
all_ride$day_of_week <- format(as.Date(all_ride$date), "%A")
Adding a new column called "ride_length" by calculating the difference in started_at and ended_at(in seconds)

all_ride$ride_length <- difftime(all_ride$ended_at,all_ride$started_at)
Inspecting the structure of all the columns
str(all_ride)
spec_tbl_df [5,723,532 × 19] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ ride_id           : chr [1:5723532] "6C992BD37A98A63F" "1E0145613A209000" "E498E15508A80BAD" "1887262AD101C604" ...
 $ rideable_type     : chr [1:5723532] "classic_bike" "docked_bike" "docked_bike" "classic_bike" ...
 $ started_at        : POSIXct[1:5723532], format: "2021-04-12 18:25:36" "2021-04-27 17:27:11" ...
 $ ended_at          : POSIXct[1:5723532], format: "2021-04-12 18:56:55" "2021-04-27 18:31:29" ...
 $ start_station_name: chr [1:5723532] "State St & Pearson St" "Dorchester Ave & 49th St" "Loomis Blvd & 84th St" "Honore St & Division St" ...
 $ start_station_id  : chr [1:5723532] "TA1307000061" "KA1503000069" "20121" "TA1305000034" ...
 $ end_station_name  : chr [1:5723532] "Southport Ave & Waveland Ave" "Dorchester Ave & 49th St" "Loomis Blvd & 84th St" "Southport Ave & Waveland Ave" ...
 $ end_station_id    : chr [1:5723532] "13235" "KA1503000069" "20121" "13235" ...
 $ start_lat         : num [1:5723532] 41.9 41.8 41.7 41.9 41.7 ...
 $ start_lng         : num [1:5723532] -87.6 -87.6 -87.7 -87.7 -87.7 ...
 $ end_lat           : num [1:5723532] 41.9 41.8 41.7 41.9 41.7 ...
 $ end_lng           : num [1:5723532] -87.7 -87.6 -87.7 -87.7 -87.7 ...
 $ member_casual     : chr [1:5723532] "member" "casual" "casual" "member" ...
 $ date              : Date[1:5723532], format: "2021-04-12" "2021-04-27" ...
 $ month             : chr [1:5723532] "04" "04" "04" "04" ...
 $ day               : chr [1:5723532] "12" "27" "03" "17" ...
 $ year              : chr [1:5723532] "2021" "2021" "2021" "2021" ...
 $ day_of_week       : chr [1:5723532] "Monday" "Tuesday" "Saturday" "Saturday" ...
 $ ride_length       : 'difftime' num [1:5723532] 1879 3858 341859 1506 ...
  ..- attr(*, "units")= chr "secs"
 - attr(*, "spec")=
  .. cols(
  ..   ride_id = col_character(),
  ..   rideable_type = col_character(),
  ..   started_at = col_datetime(format = ""),
  ..   ended_at = col_datetime(format = ""),
  ..   start_station_name = col_character(),
  ..   start_station_id = col_character(),
  ..   end_station_name = col_character(),
  ..   end_station_id = col_character(),
  ..   start_lat = col_double(),
  ..   start_lng = col_double(),
  ..   end_lat = col_double(),
  ..   end_lng = col_double(),
  ..   member_casual = col_character()
  .. )
 - attr(*, "problems")=<externalptr> 
Converting "ride_length" from Factor to numeric so we can run calculations on the data
all_ride$ride_length <- as.numeric(as.character(all_ride$ride_length))
is.numeric(all_ride$ride_length)
TRUE
Checking for negative ride time
all_ride %>% 
  filter(ended_at < started_at)
A spec_tbl_df: 145 × 19
ride_id	rideable_type	started_at	ended_at	start_station_name	start_station_id	end_station_name	end_station_id	start_lat	start_lng	end_lat	end_lng	member_casual	date	month	day	year	day_of_week	ride_length
<chr>	<chr>	<dttm>	<dttm>	<chr>	<chr>	<chr>	<chr>	<dbl>	<dbl>	<dbl>	<dbl>	<chr>	<date>	<chr>	<chr>	<chr>	<chr>	<dbl>
BC53ECCBC76278FD	classic_bike	2021-04-07 16:11:33	2021-04-07 16:11:26	Ashland Ave & Grand Ave            	13434       	Ashland Ave & Grand Ave            	13434       	41.89107	-87.66661	41.89107	-87.66661	member	2021-04-07	04	07	2021	Wednesday	  -7
209C097828F9CD43	electric_bike	2021-04-27 17:13:44	2021-04-27 17:11:32	NA	NA	NA	NA	41.91000	-87.64000	41.91000	-87.64000	member	2021-04-27	04	27	2021	Tuesday	-132
6E81034B446FC2FD	electric_bike	2021-04-23 09:43:39	2021-04-23 09:43:29	Dayton St & North Ave              	13058       	Dayton St & North Ave              	13058       	41.91064	-87.64937	41.91065	-87.64939	member	2021-04-23	04	23	2021	Friday   	-10
318DD838369AEA61	classic_bike	2021-04-30 10:56:32	2021-04-30 10:56:30	Dayton St & North Ave              	13058       	Dayton St & North Ave              	13058       	41.91058	-87.64942	41.91058	-87.64942	member	2021-04-30	04	30	2021	Friday   	  -2
8ADD13BD8F6A7567	classic_bike	2021-04-17 12:43:36	2021-04-17 12:43:27	Dayton St & North Ave              	13058       	Dayton St & North Ave              	13058       	41.91058	-87.64942	41.91058	-87.64942	member	2021-04-17	04	17	2021	Saturday	  -9
3EC1B5A4D4B9AB99	classic_bike	2021-05-05 16:10:04	2021-05-05 16:09:51	Dayton St & North Ave              	13058       	Dayton St & North Ave              	13058       	41.91058	-87.64942	41.91058	-87.64942	member	2021-05-05	05	05	2021	Wednesday	-13
518535DDFA372694	electric_bike	2021-05-20 12:31:53	2021-05-20 12:31:52	                                   	            	Ellis Ave & 60th St                	KA1503000014	41.79000	-87.60000	41.78507	-87.60108	member	2021-05-20	05	20	2021	Thursday	  -1
732D84DAD2CC9B73	classic_bike	2021-06-20 10:52:26	2021-06-20 10:52:25	Clinton St & Polk St               	15542       	Clinton St & Polk St               	15542       	41.87147	-87.64095	41.87147	-87.64095	casual	2021-06-20	06	20	2021	Sunday   	  -1
A18D39992AA99793	classic_bike	2021-06-15 20:58:03	2021-06-15 20:54:51	Broadway & Sheridan Rd             	13323       	Broadway & Sheridan Rd             	13323       	41.95283	-87.64999	41.95283	-87.64999	casual	2021-06-15	06	15	2021	Tuesday  	-192
126E4DA0FA0A3E11	electric_bike	2021-06-02 17:52:32	2021-06-02 17:47:26	NA                                 	NA          	Southport Ave & Wrightwood Ave     	TA1307000113	41.93000	-87.66000	41.92875	-87.66393	member	2021-06-02	06	02	2021	Wednesday	-306
24C4FC421D642C22	classic_bike	2021-06-28 13:18:26	2021-06-28 13:18:25	Mies van der Rohe Way & Chicago Ave	13338       	Mies van der Rohe Way & Chicago Ave	13338       	41.89691	-87.62174	41.89691	-87.62174	member	2021-06-28	06	28	2021	Monday   	  -1
4E88151C0FBCA967	classic_bike	2021-06-28 14:56:28	2021-06-28 14:56:27	Michigan Ave & Oak St              	13042       	Michigan Ave & Oak St              	13042       	41.90096	-87.62378	41.90096	-87.62378	casual	2021-06-28	06	28	2021	Monday   	  -1
E6C4F61273BC824D	classic_bike	2021-07-23 11:32:12	2021-07-23 11:32:08	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	casual	2021-07-23	07	23	2021	Friday   	  -4
18FA8EAE88922DAF	classic_bike	2021-07-21 08:02:07	2021-07-21 08:02:02	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	member	2021-07-21	07	21	2021	Wednesday	  -5
3C634446B054AB44	classic_bike	2021-07-27 19:11:55	2021-07-27 19:11:54	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	member	2021-07-27	07	27	2021	Tuesday  	  -1
D22A7B1DAC07DBEC	classic_bike	2021-07-25 01:38:23	2021-07-25 01:38:22	Walsh Park	18067	Walsh Park	18067	41.91461	-87.66797	41.91461	-87.66797	casual	2021-07-25	07	25	2021	Sunday	-1
CBBDF121760541A8	classic_bike	2021-07-24 13:46:27	2021-07-24 13:46:19	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	member	2021-07-24	07	24	2021	Saturday	  -8
9180A7126B192284	classic_bike	2021-07-18 12:27:30	2021-07-18 12:27:26	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	casual	2021-07-18	07	18	2021	Sunday   	  -4
AC7176564B0C716F	classic_bike	2021-07-20 12:52:08	2021-07-20 12:52:02	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	casual	2021-07-20	07	20	2021	Tuesday  	  -6
B30086B9F4A40A93	classic_bike	2021-07-25 11:14:54	2021-07-25 11:14:50	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	casual	2021-07-25	07	25	2021	Sunday   	  -4
2C8922585E5F5B76	classic_bike	2021-07-19 18:15:41	2021-07-19 18:15:36	Racine Ave & Wrightwood Ave        	TA1309000059	Racine Ave & Wrightwood Ave        	TA1309000059	41.92889	-87.65897	41.92889	-87.65897	casual	2021-07-19	07	19	2021	Monday   	  -5
F15EA3F8AB85D605	classic_bike	2021-07-12 18:22:49	2021-07-12 18:22:37	Damen Ave & Clybourn Ave           	13271       	Damen Ave & Clybourn Ave           	13271       	41.93193	-87.67786	41.93193	-87.67786	member	2021-07-12	07	12	2021	Monday   	-12
C74A0859A1737B0F	classic_bike	2021-07-07 10:38:25	2021-07-07 10:38:21	Damen Ave & Clybourn Ave           	13271       	Damen Ave & Clybourn Ave           	13271       	41.93193	-87.67786	41.93193	-87.67786	casual	2021-07-07	07	07	2021	Wednesday	  -4
2AB142C32C184032	electric_bike	2021-07-07 18:51:53	2021-07-07 18:51:45	Damen Ave & Clybourn Ave           	13271       	Damen Ave & Clybourn Ave           	13271       	41.93183	-87.67776	41.93184	-87.67779	casual	2021-07-07	07	07	2021	Wednesday	  -8
FEA10221DC06E355	electric_bike	2021-07-24 11:17:09	2021-07-24 11:17:06			Valli Produce - Evanston Plaza	599	42.04000	-87.70000	42.03971	-87.69944	member	2021-07-24	07	24	2021	Saturday	-3
A2DBE0C0012129B1	classic_bike	2021-08-20 16:19:52	2021-08-20 16:19:16	Sheffield Ave & Fullerton Ave      	TA1306000016	Sheffield Ave & Fullerton Ave      	TA1306000016	41.92560	-87.65371	41.92560	-87.65371	member	2021-08-20	08	20	2021	Friday   	-36
0291C81C6932E735	electric_bike	2021-08-20 16:20:35	2021-08-20 16:19:37	Streeter Dr & Grand Ave            	13022       	Streeter Dr & Grand Ave            	13022       	41.89230	-87.61224	41.89228	-87.61226	casual	2021-08-20	08	20	2021	Friday   	-58
4DD89B8847CF6040	electric_bike	2021-08-10 09:32:21	2021-08-10 09:31:11	Rush St & Superior St              	15530       	NA                                 	NA          	41.89590	-87.62578	41.90000	-87.63000	casual	2021-08-10	08	10	2021	Tuesday  	-70
ACD13D8A68452042	classic_bike	2021-08-21 14:08:50	2021-08-21 14:08:27	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	casual	2021-08-21	08	21	2021	Saturday	-23
2F600E738BE2F08A	classic_bike	2021-08-21 14:10:29	2021-08-21 14:10:08	Halsted St & Dickens Ave           	13192       	Halsted St & Dickens Ave           	13192       	41.91994	-87.64883	41.91994	-87.64883	casual	2021-08-21	08	21	2021	Saturday	-21
⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮	⋮
9BEB5FBD0EF2FCFD	electric_bike	2021-11-07 01:55:32	2021-11-07 01:11:50	Wabash Ave & Adams St                 	KA1503000015	May St & Taylor St                    	13160       	41.87958	-87.62605	41.86941	-87.65534	member	2021-11-07	11	07	2021	Sunday  	-2622
FD8AF7324ABAE9DA	electric_bike	2021-11-07 01:56:51	2021-11-07 01:00:57	Clark St & North Ave                  	13128       	Larrabee St & Webster Ave             	13193       	41.91174	-87.63215	41.92176	-87.64403	casual	2021-11-07	11	07	2021	Sunday  	-3354
1374B0438900E9E9	classic_bike	2021-11-07 01:52:15	2021-11-07 01:25:56	Orleans St & Hubbard St               	636         	Clark St & Drummond Pl                	TA1307000142	41.89003	-87.63662	41.93125	-87.64434	member	2021-11-07	11	07	2021	Sunday  	-1579
E17513A83D75F889	electric_bike	2021-11-07 01:50:18	2021-11-07 01:03:54	                                      	            	Wilton Ave & Diversey Pkwy            	TA1306000014	41.90000	-87.63000	41.93248	-87.65276	casual	2021-11-07	11	07	2021	Sunday  	-2784
CF4D877FEB218570	electric_bike	2021-11-07 01:45:48	2021-11-07 01:08:54	Major Taylor Trail & 115th St         	20207       	                                      	            	41.68496	-87.64527	41.67000	-87.64000	member	2021-11-07	11	07	2021	Sunday  	-2214
E394AA8418D47B74	electric_bike	2021-11-07 01:50:56	2021-11-07 01:20:21	Damen Ave & Pierce Ave                	TA1305000041	Wilton Ave & Belmont Ave              	TA1307000134	41.90937	-87.67784	41.93997	-87.65311	casual	2021-11-07	11	07	2021	Sunday  	-1835
9D8C6B064E2ECEDE	classic_bike	2021-11-07 01:54:37	2021-11-07 01:04:33	Wells St & Concord Ln                 	TA1308000050	Broadway & Barry Ave                  	13137       	41.91213	-87.63466	41.93758	-87.64410	casual	2021-11-07	11	07	2021	Sunday  	-3004
984A42435A4BBEB0	electric_bike	2021-11-07 01:49:38	2021-11-07 01:03:11	Wood St & Milwaukee Ave               	13221       	Halsted St & Dickens Ave              	13192       	41.90758	-87.67247	41.91983	-87.64926	casual	2021-11-07	11	07	2021	Sunday  	-2787
83778DB379E8B04B	electric_bike	2021-11-07 01:54:08	2021-11-07 01:12:16	                                      	            	Campbell Ave & Fullerton Ave          	15648       	41.90000	-87.63000	41.92464	-87.68931	member	2021-11-07	11	07	2021	Sunday  	-2512
D6D3692804119896	classic_bike	2021-11-07 01:54:00	2021-11-07 01:05:08	Franklin St & Illinois St             	RN-         	Michigan Ave & Pearson St             	13034       	41.89102	-87.63548	41.89766	-87.62351	member	2021-11-07	11	07	2021	Sunday  	-2932
1E08692D5C77F7AA	classic_bike	2021-11-07 01:38:12	2021-11-07 01:02:11	Milwaukee Ave & Wabansia Ave          	13243       	Greenview Ave & Diversey Pkwy         	13294       	41.91262	-87.68139	41.93259	-87.66594	casual	2021-11-07	11	07	2021	Sunday  	-2161
7E24361D78747AF6	electric_bike	2021-11-07 01:58:06	2021-11-07 01:06:43	Wells St & Walton St                  	TA1306000011	Clark St & Randolph St                	TA1305000030	41.89995	-87.63445	41.88526	-87.63231	member	2021-11-07	11	07	2021	Sunday  	-3083
6F9E76F5EDAAC1B8	electric_bike	2021-11-07 01:55:42	2021-11-07 01:01:55	Milwaukee Ave & Wabansia Ave          	13243       	Western Ave & Division St             	13241       	41.91258	-87.68142	41.90291	-87.68737	member	2021-11-07	11	07	2021	Sunday  	-3227
F2AF011E90AC8918	classic_bike	2021-11-07 01:53:03	2021-11-07 01:22:34	Orleans St & Hubbard St               	636         	Broadway & Belmont Ave                	13277       	41.89003	-87.63662	41.94011	-87.64545	casual	2021-11-07	11	07	2021	Sunday  	-1829
7AECC76D1562B51C	classic_bike	2021-11-07 01:54:58	2021-11-07 01:01:29	Sheffield Ave & Wrightwood Ave        	TA1309000023	Southport Ave & Wellington Ave        	TA1307000006	41.92871	-87.65383	41.93573	-87.66358	casual	2021-11-07	11	07	2021	Sunday  	-3209
36198116E86D6457	electric_bike	2021-11-07 01:57:36	2021-11-07 01:16:31	Wilton Ave & Belmont Ave              	TA1307000134	St. Clair St & Erie St                	13016       	41.94003	-87.65295	41.89516	-87.62331	member	2021-11-07	11	07	2021	Sunday  	-2465
3556173EA13B5C84	electric_bike	2021-11-07 01:53:22	2021-11-07 01:05:08	Ashland Ave & Grace St                	13319       	                                      	            	41.95065	-87.66874	41.94000	-87.70000	casual	2021-11-07	11	07	2021	Sunday  	-2894
49DF29FDEC7E48FB	electric_bike	2021-11-07 01:55:34	2021-11-07 01:08:44	Logan Blvd & Elston Ave               	TA1308000031	                                      	            	41.92949	-87.68421	41.94000	-87.65000	casual	2021-11-07	11	07	2021	Sunday  	-2810
214464733718183D	electric_bike	2021-11-07 01:37:57	2021-11-07 01:13:17					41.88000	-87.62000	41.80000	-87.59000	casual	2021-11-07	11	07	2021	Sunday	-1480
658F94C7AE8F182C	electric_bike	2021-11-07 01:42:19	2021-11-07 01:03:58					41.79000	-87.60000	41.79000	-87.60000	member	2021-11-07	11	07	2021	Sunday	-2301
53222CFE6657D53D	electric_bike	2021-11-07 01:52:22	2021-11-07 01:01:29	Milwaukee Ave & Fullerton Ave         	428         	                                      	            	41.92000	-87.70000	41.91000	-87.71000	casual	2021-11-07	11	07	2021	Sunday  	-3053
D2220642A2BF783C	electric_bike	2021-11-07 01:26:28	2021-11-07 01:08:35					41.86000	-87.63000	41.95000	-87.65000	member	2021-11-07	11	07	2021	Sunday	-1073
36CAA82BB5852EF4	electric_bike	2021-11-07 01:19:04	2021-11-07 01:00:27					41.75000	-87.61000	41.75000	-87.57000	member	2021-11-07	11	07	2021	Sunday	-1117
287605D0D79731E6	electric_bike	2021-11-07 01:49:11	2021-11-07 01:13:26					41.93000	-87.65000	41.97000	-87.70000	casual	2021-11-07	11	07	2021	Sunday	-2145
8598DCE30427F984	electric_bike	2021-11-07 01:31:33	2021-11-07 01:03:44	Orleans St & Elm St                   	TA1306000006	                                      	            	41.90292	-87.63771	41.93000	-87.66000	casual	2021-11-07	11	07	2021	Sunday  	-1669
5AA2BC364BC7A569	electric_bike	2021-11-07 01:59:53	2021-11-07 01:09:02					41.92000	-87.69000	41.90000	-87.70000	casual	2021-11-07	11	07	2021	Sunday	-3051
F4E4485BFB33D916	electric_bike	2021-11-07 01:57:53	2021-11-07 01:27:02					41.91000	-87.72000	41.90000	-87.77000	casual	2021-11-07	11	07	2021	Sunday	-1851
B506DCD44974C575	electric_bike	2021-11-07 01:53:34	2021-11-07 01:00:42	Milwaukee Ave & Fullerton Ave         	428         	                                      	            	41.92000	-87.70000	41.91000	-87.71000	casual	2021-11-07	11	07	2021	Sunday  	-3172
2D97E3C98E165D80	classic_bike	2022-03-05 11:00:57	2022-03-05 10:55:01	DuSable Lake Shore Dr & Wellington Ave	TA1307000041	DuSable Lake Shore Dr & Wellington Ave	TA1307000041	41.93669	-87.63683	41.93669	-87.63683	casual	2022-03-05	03	05	2022	Saturday	-356
7407049C5D89A13D	electric_bike	2022-03-05 11:38:04	2022-03-05 11:37:57	Sheffield Ave & Wellington Ave        	TA1307000052	Sheffield Ave & Wellington Ave        	TA1307000052	41.93631	-87.65252	41.93625	-87.65266	casual	2022-03-05	03	05	2022	Saturday	   -7
There are 145 negative rows of time values. These might have been due to data collection error. I'll have to remove it as it might skew the result of my analysis

Removing "bad" data
The dataframe includes a few negative time entries where ride_length was negative, so it needs to be filtered out. We will create a new version of the dataframe (all_ride2) since data is being removed.

all_ride2 <- all_ride %>% 
  filter(ended_at > started_at) 

glimpse(all_ride2)
Rows: 5,722,873
Columns: 19
$ ride_id            <chr> "6C992BD37A98A63F", "1E0145613A209000", "E498E15508…
$ rideable_type      <chr> "classic_bike", "docked_bike", "docked_bike", "clas…
$ started_at         <dttm> 2021-04-12 18:25:36, 2021-04-27 17:27:11, 2021-04-…
$ ended_at           <dttm> 2021-04-12 18:56:55, 2021-04-27 18:31:29, 2021-04-…
$ start_station_name <chr> "State St & Pearson St", "Dorchester Ave & 49th St"…
$ start_station_id   <chr> "TA1307000061", "KA1503000069", "20121", "TA1305000…
$ end_station_name   <chr> "Southport Ave & Waveland Ave", "Dorchester Ave & 4…
$ end_station_id     <chr> "13235", "KA1503000069", "20121", "13235", "20121",…
$ start_lat          <dbl> 41.89745, 41.80577, 41.74149, 41.90312, 41.74149, 4…
$ start_lng          <dbl> -87.62872, -87.59246, -87.65841, -87.67394, -87.658…
$ end_lat            <dbl> 41.94815, 41.80577, 41.74149, 41.94815, 41.74149, 4…
$ end_lng            <dbl> -87.66394, -87.59246, -87.65841, -87.66394, -87.658…
$ member_casual      <chr> "member", "casual", "casual", "member", "casual", "…
$ date               <date> 2021-04-12, 2021-04-27, 2021-04-03, 2021-04-17, 20…
$ month              <chr> "04", "04", "04", "04", "04", "04", "04", "04", "04…
$ day                <chr> "12", "27", "03", "17", "03", "25", "03", "06", "12…
$ year               <chr> "2021", "2021", "2021", "2021", "2021", "2021", "20…
$ day_of_week        <chr> "Monday", "Tuesday", "Saturday", "Saturday", "Satur…
$ ride_length        <dbl> 1879, 3858, 341859, 1506, 5477, 41, 86, 1550, 3174,…
Removing null values
all_ride2 <- all_ride2 %>% 
  na.omit()
After removing the null values, we check our dataframe to see what we have. 542,718 rows have been removed.

STEP 4: CONDUCTING DESCRIPTIVE ANALYSIS
Doing descriptive analysis on ride_length (all figures in seconds) to check for the average, midpoint, longest ride and shortest ride

all_ride2 %>% 
  summarise(mean=mean(ride_length), median=median(ride_length), max=max(ride_length), min=min(ride_length))
#average ride-length is 1252.888, median of 709, maximum of 3,356,649 and minimum of 1 sec
A tibble: 1 × 4
mean	median	max	min
<dbl>	<dbl>	<dbl>	<dbl>
1252.888	709	3356649	1
Renaming variables for easy identification
all_ride2 <- all_ride2 %>% 
  rename(ride_type = rideable_type, # changing rideable_type col to ride_type
         membership_type = member_casual)   # changing member_casual col to membership_type col
Comparing the mean, median, max and min for members and casual users
aggregate(all_ride2$ride_length ~ all_ride2$membership_type, FUN = mean)
aggregate(all_ride2$ride_length ~ all_ride2$membership_type, FUN = median)
aggregate(all_ride2$ride_length ~ all_ride2$membership_type, FUN = max)
aggregate(all_ride2$ride_length ~ all_ride2$membership_type, FUN = min)
### here, we can see th casual riders having an average of 1,846 sec ride length while the member riders have 782 sec ride length.
### median for casual riders is 964 secs while for member riders is 565
### maximum ride length for casual riders is 3,356,649 while for the member riders is 89,996
### they both have minimum of 1 sec ride length
A data.frame: 2 × 2
all_ride2$membership_type	all_ride2$ride_length
<chr>	<dbl>
casual	1846.3636
member	782.0501
A data.frame: 2 × 2
all_ride2$membership_type	all_ride2$ride_length
<chr>	<dbl>
casual	964
member	565
A data.frame: 2 × 2
all_ride2$membership_type	all_ride2$ride_length
<chr>	<dbl>
casual	3356649
member	89996
A data.frame: 2 × 2
all_ride2$membership_type	all_ride2$ride_length
<chr>	<dbl>
casual	1
member	1
Calculating the average ride time by each day for members vs casual users
aggregate(all_ride2$ride_length ~ all_ride2$membership_type + all_ride2$day_of_week, FUN = mean)
### from here, it is seen that both the casual riders and member riders rode more on sundays. Although, the Casual riders rode more with a ride length of 2,162 secs compared to member riders with 896 secs ride length. Also, the member riders ride as much during the weekdays.
A data.frame: 14 × 3
all_ride2$membership_type	all_ride2$day_of_week	all_ride2$ride_length
<chr>	<chr>	<dbl>
casual	Friday	1756.6704
member	Friday	766.1274
casual	Monday	1835.9485
member	Monday	758.2399
casual	Saturday	1989.7090
member	Saturday	876.1887
casual	Sunday	2161.3381
member	Sunday	896.2450
casual	Thursday	1602.9612
member	Thursday	736.2140
casual	Tuesday	1612.7899
member	Tuesday	730.8352
casual	Wednesday	1616.1174
member	Wednesday	742.4541
Putting the days of the week in order

all_ride2$day_of_week <- ordered(all_ride2$day_of_week, levels=c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))
PHASE 4:ANALYZING AND VISUALIZATION
checking for the count of members and casual riders
table(all_ride2$membership_type)
table(all_ride2$ride_type)

### visualizing the membership_type count
ggplot(data=all_ride2)+ geom_bar(mapping=aes(x=membership_type, fill = membership_type)) +
labs(title = 'Member and Casual Membership Count',
    x = 'Membership type',
    y = 'Count')
### Here number of casual riders-> 2,291,630
### Number of member riders -> 2,888,525 i.e. we have more member riders compared to casual riders.
### Also according to the ride type, we have 3,243,934 classic bike, 303,515 docked bike and 1,632,706 electric bike.
 casual  member 
2291630 2888525 
 classic_bike   docked_bike electric_bike 
      3243934        303515       1632706 

### plotting a graph to better visualize the result
ggplot(data=all_ride2)+geom_bar(mapping=aes(x = ride_type, fill=ride_type)) +
  facet_wrap(~membership_type) +
  labs(title = 'Count of Casual and Member based on Ride_type', 
       x = 'Ride Type',
       y = 'Count')
### here, we can see the member riders use more of the classic bike  compared to the electric bike. non of its riders use the docked bike. For the Casual riders, more use the classic bikes, followed by the electric bike, then the docked bike.

### Analyzing and visualizing ridership data by type and weekday
all_ride2 %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>%  #creates weekday field using wday()
  group_by(membership_type, weekday) %>%  #groups by usertype and weekday
  summarize(number_of_rides = n()							#calculates the number of rides and average duration 
  ,average_duration = mean(ride_length)) %>% 		# calculates the average duration
  arrange(membership_type, weekday) %>% 
ggplot(aes(x = weekday, y = number_of_rides, fill = membership_type)) +
  geom_col(position = "dodge")
# here, it shows the number of rides among the riders during the weekday, casual riders have the highest number of rides during the saturday while member ridershave highest number on wednesday.
`summarise()` has grouped output by 'membership_type'. You can override using
the `.groups` argument.

# Analyzing and visualizing ridership data by type and month

all_ride2 %>% 
  mutate(month = month(started_at, label = TRUE)) %>%  #creates month field using month()
  group_by(membership_type, month) %>%  #groups by membership_type and month
  summarize(number_of_rides = n()							#calculates the number of rides and average duration 
  ,average_duration = mean(ride_length)) %>% 		# calculates the average duration
  arrange(membership_type, month) %>% 
ggplot(aes(x = month, y = number_of_rides, fill = membership_type)) +
  geom_col(position = "dodge")
# casual riders have low number of rides from the beginning of the year(i.e. january - apr), it start picking up from may to september with the peak during the month of july, then it starts declining after september while member riders have low number of rides from the beginning of the year(i.e. january - febuary), it normalises and ranges during march to september with the peak during the month of september, then it starts declining after september.
`summarise()` has grouped output by 'membership_type'. You can override using
the `.groups` argument.

# Visualizing average duration

all_ride2 %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>% 
  group_by(membership_type, weekday) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(membership_type, weekday)  %>% 
  ggplot(aes(x = weekday, y = average_duration, fill = membership_type)) +
  geom_col(position = "dodge")
`summarise()` has grouped output by 'membership_type'. You can override using
the `.groups` argument.

PHASE 5 - SHARE
Conclusions: From the analysis, we could deduce the following observations: The casual riders have the most ride length i.e. they ride the most.casual riders are seen to be very active during the weekends (i.e. Saturday and Sunday) While member riders have the most ride length on sunday, it is also evenly distributed across the week which indicates they ride as much during the week. Generally, We have more member riders compared to casual riders in the membership.Also according to the ride type, we have 3,243,934 classic bike, 303,515 docked bike and 1,632,706 electric bike.The member riders use more of the classic bike compared to the electric bike. non of its riders use the docked bike. For the Casual riders, more use the classic bikes, followed by the electric bike, then the docked bike. Casual riders have the highest number of rides during saturday followed by sunday while member riders have the number of rides spread during the week with peak on wednesday.Casual and member riders are seen to be more active between July and September *Casual riders have more than 2 times average duration than the member riders.

Recommendation
The marketing team can create a new campaign for the annual membership plan that would enable riders have more access to weekday rides as well as weekend rides at a subsidized price. Ads could be created outlining the benefits of using bikes daily especially during the weekdays either to commute to work or just to move around the city - focusing on its benefits in order to lure the casual riders into riding during the week as they are the ones that ride most.

Also, a membership plan could also be created for the casual riders who love to ride on weekends only that allows them pay for their subscription like the annaul member rider but only access the bikes on weekends.By doing this, it will save them some money as their subscription will be done annually while generating more income for the company by converting them into annual members.

Incentives and discount should be given to casual riders who decides to subcribe to the annual membership plan as a way to lure the other casual riders into annual rider
