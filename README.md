# Waiting for a psychologist in Midtjylland
This is a repository for my final project in spatial analysis 2023. This repo will contain the data, scripts etc. use for creating the project. 

## 1. Description and purpose
If you need a psychologist in Midtjylland, you might have to wait many months to get one. The many weeks of waiting can cause the mental issues of the waiting patients to worsen, which can result in the patient living with his or her issues for a longer peiod of time and maybee needing medical pf psykiatric treatment, which could have been avoided (Ching-I Hung 2017, 7). The longer the patient is sick the more expensive it si for society to pay for this treatment, and it also costs society a lot of money in lost production (Flachs EM 2015, 163-195). The waiting time and thereby the risk of getting a more serious course of illness is not equally distributed through the municipalities, which makes the waiting time not only a problem for the individual patient, but also a problem of inequality. 

The purpose of this project is to use spatial tools to investigate the waiting times to see, which municipalities has the longest waiting times, and how many people live in these "vulnerable" areas and can therefore risk to be affected by the long waits. I expect that the municipalities with the longest waiting time also are the ones with the biggest population and the ones with the most people per psychology practice, because an imbalance between supply and demand could then explan why the waiting times vary from municipality to municipality. I create four different maps to investigate this hypothesis. 

__Output:__ The output of this project is
- 3 fugures (4 maps). Saved in ```map_output``` folder. 
- a Rmarkdown file with the script made in RStudio. Saved in ```scripts``` folder. 
- a HTML version of the Rmarkdown. Saved in ```scripts``` folder.
- the project report. Saved in ```report``` folder. 
- a data set called ```waiting_midt.csv```, which is the project relevant data from each of the four data sets merged into one data set. Saved in ```data_output``` folder. 

## 2. Methods

I have create three figues consisting of four maps to shed light over the waiting time problem in Midtjylland. 
1) Figure 1 is a map created with ```Mapview``` and it's an interactive map which makes it possible to click on each municipality and get its name and some facts about the average, min and max waiting. The colours are ranging from red to blue and indicates the length of the waiting times. My biggest challenge using Mapview was to costumize the legend and chose the column values which I wanted to be shown when the user clicked on a municipality. 

2) Figure 2 is two maps: one showing the waiting times in each municipality, and one showing the size of the adult population (18-125 years). These maps makes it possible to investigate wether the municipalities with the longest waiting times are also the ones with the biggest population and vice versa. The maps are created with different ```tmap``` functions. 

3) Figure 3 is the waiting time map mentioned above, but bubbles are added using ```tm_bubbles()``` to illustrate the number of citizens per practice in each municipality. This map makes it possible to investigate wether the municipalities with the longest waiting time are also the municipalities with the most people per practice and vice versa. I didn't manage to edit the title of the second legend (the one describing the bubble sizes), so the header is just the name of the column. 

Other spatial commands:
- I used the function ```st_as_sf()``` to convert the "Midtjylland" data frame into a simple features (sf) object.
- I projected the "Midtjylland" data by assigning it to the CRS connected to the EPSG code 25832 using ```st_transform()```. This made me able to map on a 2D surface insteda of a 3D globe. The EPSG code is the one most commonly used for mapping Denmark. 
- I found the centroid of each municipality with ```st_centroid()```. The centroids were used to place the bubbles in the center of each municipality. 

## 3. Data
In this project I have worked with four data sets:

1) The ```municipalities``` data is from the GADM database. I use the geometry of each municipality in Denmark, and they are loaded directly from the database into the script in RStudion. 

2) ```waitingtime_regionmidt.csv``` contains the average, maximum and minimum waiting times for each of the 19 municipalities in Midtjylland from November 1st, 2021. The numbers are from a report written by Region Midt in March 2022. The waiting times are measured in weeks. They apply to non-urgent patients who fall under cause 10 (light to moderate depression) or 11 (light to moderate anxiety) (Region Midtjylland 2022,4). I created the data set on my own by writing the data and the headings from the report into an excel document and saved it as a csv. The data has the following columns: "kommune" (municipalitiy), "Maksimum pr. 1. Nov 2021" (maximum November 1st, 2021), and "Minimum pr. 1. Nov 2021" (minimum November 1st, 2021). 

3) The ```population_over_18.csv``` data set is from Danmarks Statistik. It contains the number of citizens from age 18-125  in the 19 municipalities in Midtjylland. I have chosen only the adult population, because the waiting times from waitingtime_regionmidt.csv only applies to persons older than 18, while the waiting time for children below 18 might be different. The population is from October 1st 2021. Following the link, you get to page “Folketal den 1. i kvartalet efter køn, tid, område og alder” (population on the 1s of the quarter by sex, time, area, and age) on dst.dk. To get the data, I selected all ages above 18, all municipalities in Region Midtjylland, "i alt" (total) in the "køn" (gender) box, and "“2021K4” (the 4th quarter of 2021) in the "Kvartal" (quarter) box. After I downloaded the data, I removed the word “år” (year) from each age so only the age number was left, because otherwise RStudio couldn't interpret the data (Danmarks Statistik 2021). 

4) The data in the ```psycology_practices_2018.csv``` is from a report by Region Midtjylland (Region Midtjylland 2019, 12). I assembled the data set myself by writing the numbers from the report into an excel document and saving it as a csv. I named the headings “municipality” and “practices”. The numbers are from November 2018.  

### 3.1 How to get data 
1) load the data directly from GADM with ```get_Data()```
      
      getData("GADM", country = "DNK", level = 2)
      
2-4) Data set 2-4 are saved in the ```data``` folder in the GitHub repository. They are loaded into the script with the function ```read.csv2()```

## 4. Usage

### 4.1 Prerequisites
The code has been developed and tested in RStudio 2022.12.0+353 in a macOS Monterey 12.6.3 computer. 

### 4.2 Install packages
The required packages are installed when the script is run from the top. The packages needed are: 
- sf 
- raster
- dplyr
- mapview
- RColorBrewer 
- tmap

### 4.3 How to tun script
The script ans the project is located in the ```scripts``` folder in the GitHub repository. The script should be loaded into RStudio and run from the top. 

## 5. Discussion of results 
The empirical results and a critical evaluation can be found in the project report in the ```report``` folder. 

## 6. References
Ching-I Hung et al.
2017	”Untreated duration predicted the severity of depression at the two-year follow-up point”, PLoS ONE 12(9).  

Danmarks Statistik
2021	Population data, “Folk1A: Folketal den 1. i kvartaletefter område, køn, alder og civiltilstand”: https://www.statistikbanken.dk/statbank5a/selectvarval/define.aspPLanguage=0&subword=tabsel&MainTable=FOLK1A&PXSId=199114&tablestyle=&ST=SD&buttons=0 
 (visited 2023-06-02)

Flachs EM et al. 
2015	“Sygdomsbyrden i Danmark - sygdomme”, Statens institut for folkesundhed, Syddansk Universitet, København: Sundhedsstyrelsen, 163-195: https://www.sst.dk/da/sygdom-og-behandling/~/media/00C6825B11BD46F9B064536C6E7DFBA0.ashx 

Region Midtjylland
2019	”Praksisplan for psykologer”, 
https://www.rm.dk/siteassets/politik/udvalg/samarbejdsudvalg-for-primar-sektoren/psykologer/praksisplan-for-psykologer-2019.pdf 

Region Midtjylland
2022	”Fakta om psykologyderområdet i Region Midtjylland”, https://www.rm.dk/api/NewESDHBlock/DownloadFile?agendaPath=%5C%5CRMAPPS0221.onerm.dk%5CCMS01-EXT%5CESDH%20Data%5CRM_Internet%5Cdagsordener%5Cregionsraadet%202022%5C26-01-2022%5CAaben_dagsorden&appendixId=330776 


