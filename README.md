# 11464537ERP

1. Title
Ward Typology for Community Resilience.

2. Description

This project presents a comprehensive analysis and development of a ward-level typology for community resilience in England using a novel approach called Topological Data Analysis Ball Mapper (TDABM), to cluster wards using identified community resilience characteristics for the analysis of the groups of wards within England. The project offers valuable insights into the diversity and complexity of community profiles across England.

The typology developed is intended to inform resilience planning and intervention strategies, providing a granular understanding of Englands different community types. The project compares the outcomes of the TDABM with a traditional k-means clustering method, highlighting the strengths and limitations TDABM in capturing the unique characteristics of community resilience.

This research contributes to both fields,the field of community resilience by offering a detailed, data-driven approach to understanding how different communities can be grouped based on resilience features, which can be critical for targeted policy-making, and Topological Data Analysis by highlighting its abilities and potential use in Social Sciences.

3. Table of Contents

    1. Title
    2. Description
    3. Table of Contents
    4. Usage
    5. Data
    6. Scripts description
    7.Note
    
4. Usage
To run the analysis, ensure you have the necessary datasets (as outlined in the Data section). The scripts to use are:

    ERP_part1_PreparingData.ipynb - The goal is to prepare the data and create two DF, one for clustering without dummy variables and another one withthem.
    
    ERP_part2_TDABallmapper.ipynb - The goal is to use the Topological Data Analysis Ballmapper (TDABM) to study the typology of wards. 
    
    ERP_part3_kmeans5.ipynb - The goal is to use the k- means clustering with a k value calculated by the elbow mehotd to study the typology of wards. 
    
    ERP_part4_kmeans21.ipynb - The goal is to use the k- means clustering with a k value calculated by the TDABM to study the typology of wards. 

5. Data
They are all Open data sources

    ERP_part1_PreparingData.ipynb :

    GeoMapa of UK: Wards_December_2022/WD_DEC_2022_UK_BFE.shp - https://www.data.gov.uk/dataset/17b77fff-9318-4bd7-a07b-622549f03dea/wards-december-2022-boundaries-uk-bfe

    UK postcodes: NSPL21_NOV_2023_UK.csv - https://geoportal.statistics.gov.uk/datasets/b4b8589b4adb40d08e22237f83456d57/about

    GP practices information: epraccur.csv - https://digital.nhs.uk/services/organisation-data-service/export-data-files/csv-downloads/gp-and-gp-practice-related-data

    Pharmacies practices information: pharmacy.csv - https://opendata.nhsbsa.net/dataset/consolidated-pharmaceutical-list/resource/60da93f7-3100-4ce1-995f-f2dcfb766949

    Primary Schools: primary_schools.csv- https://get-information-schools.service.gov.uk/Establishments/Search?SelectedTab=Establishments&SearchType=EstablishmentAll&SearchType=EstablishmentAll&OpenOnly=true&TextSearchModel.AutoSuggestValue=&f=true&b=1&b=4

    Universities: universities.csv https://get-information-schools.service.gov.uk/Establishments/Search?SelectedTab=Establishments&SearchType=EstablishmentAll&SearchType=EstablishmentAll&OpenOnly=true&TextSearchModel.AutoSuggestValue=&f=true&b=1&b=4

    Airports: 1a856d1c-9bf7-4ceb-84b5-f172b938f7b72020411-1-tt9867.jioj.shp-  https://assets.publishing.service.gov.uk/media/5c067bcb40f0b6705cfbde35/avi0109.pdf

    Census Data- Available at https://www.nomisweb.co.uk/sources/census_2021_ts

        Population Density: TS006_Population_density

        Sex: TS008_Sex.xlsx

        Number of Household: TS041_Number_of_Households.xlsx

        Ethnic group: TS021_1 - Ethnic group.xlsx

        Country of Birth: TS004 - Country of birth.xlsx

        General Health:TS037 - General health.xlsx

        Age by single year: TS007 _Age_by_single_year.csv

        Household by depravation dimensions: TS011_Householdsbydeprivationdimensions.csv"

        Socio-economic classification:  TS062_NS-SeC.csv

        Higheste level of Education attained: TS067_Highestlevelofqualification .csv

        Economic activity status: TS066 - Economic activity status.csv

        Tenure: TS054_Tenure.csv



6.Scripts description

ERP_part1_PreparingData.ipynb

    1.The name and code of wards can change from census to census, so we first create a df of wards and wardcodes from the 2021 census to use as a reference  
    2. We upload the Geodata to create maps of england
    3. We upload the postcode data of Enlgand to use as an intermediary for merging
    4. We upload the dataframes the infrasestructure data that does not come from the census data
    5.We upload the variables that come from the 2021 census data.
    6. We merge census 2021 variables, do some basic statistics, merge and delete unnecesary columns
    7. We merge the census df with the Infrastructure df, cap outliers, do some basic statistics
    8. Duplicate the DF and add dummy variables bases on community resilience literature
    9. we end up with 2 DF one for clustering without the dummy variables, and another with them
  
ERP_part2_TDABallmapper.ipynb

    1. We upload wards data, Geodata for mapping uk and both final dataframes created on ERP_part1_PreparingData.ipynb
    2. We scale the features in the dataset df using the StandardScaler
    3. We Run the ballmapper algorithm and create an itereation of the graph with hue set to all the dummy variables as seen in FIGURE 1 OF THE ERP
    4. To the df with the dummy variables we add the number of the balls generated by the TDABM
    5. We create a new df with only the dummy variables and run some statistics
    6. We calculate the mean of the standarized DF and the not standarized DF
    7. We create graphs and tables to understand the behaviour of the balls in the following order:
            7.1 TABLE 4 IN ERP
            7.2 FIGURE 2A
            7.3 FIGURE 2B
            7.4 TABLE 6 
            7.5 FIGURE 9.A
            7.6 FIGURE 9.B
            7.7 GRAPH 12.A         
    8. We create a DF for each ball and merge with the UK Geodata to create maps of each ward as seen in FIGURES : 3,4,5,6,7,8 OF THE ERP and FIGURES 13 and 14 OF THE APPENDIX on the ERP
    
ERP_part3_kmeans5.ipynb

    1. We upload wards data, Geodata for mapping uk and both final dataframes created on ERP_part1_PreparingData.ipynb
    2. We scale the features in the dataset df using the StandardScaler
    3. We run the elbow method and graph it as seen in FIGURE 10 of the ERP
    4. Based on the elbow method result we ran the k-means model
    5. We visualize the data segmentation by runing the Principal Component Analysis as seen in FIGURE 11.A of the ERP
    6. To the df with the dummy variables we add the number of the clusters generated by the k-means
    7. As a ward can only belong to one cluster, we generate a map of Uk with hue set to cluster as seen in FIGURE 15 OF THE APPENDIX on the ERP
    8. We calculate the same statistics for the overall understanding of the clustering
    
ERP_part4_kmeans21.ipynb
    1. We upload wards data, Geodata for mapping uk and both final dataframes created on ERP_part1_PreparingData.ipynb
    2. We scale the features in the dataset df using the StandardScaler
    3. Based on the number of balls generated by the TDABM we ran the k-means model
    5. We visualize the data segmentation by runing the Principal Component Analysis as seen in FIGURE 11.B of the ERP,
    6. To the df with the dummy variables we add the number of the clusters generated by the k-means
    7. As a ward can only belong to one cluster, we generate a map of Uk with hue set to cluster as seen in FIGURE 16 OF THE APPENDIX on the ERP
    8. We calculate the same statistics and generate the same graphs as part 2.


7.Note:
This project was developed as an Extended Research Project Report Submitted to the University of Manchester for the Degree of MSc in Data Science in the Faculty of Humanities. 
