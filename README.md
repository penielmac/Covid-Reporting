#covid reporting
sql connection 
server: covidrepo1-sqpdb.database.windows.net
id: adm
psw: Jeepsy@13


--------------------------------------------------
sa - storage account
dl - data lake 
ls - link service
ds - dataset
pl - pipeline
blob - blobstorage
dls - data lake storage
sa - storage account
gz - file type(zip)
tsv - file type (tab separated value)

-------------------------------
ls_blob_covidereportingsa
--------------------------------
---------------------------------

------FOR CONNECTION (link)------------------------------------------
Manage(left bar, 4th from the top) - Linked Services(in connections) - new

ls_blob_covidereportingsa
ls_blob_covidreportingdl

------FOR DATASETS--------------
SOURCE DATASET - DATA STORAGE

Author(left bar, 2nd from the top) - Datasets - New dataset - Azure blob storage - DelimitedText - linkedservices(select created link services) - File path(select uploaded file path)  - first row as header - Import schema (none - we are not manipulating the data)

ds_population_raw_gz

after opening the data set file - 
compression type(gzip) - compression level(optimal) - column delimiter(Tab\t)


TARGET DATASET - DATA LAKE
Author(left bar, 2nd from the top) - Datasets - New dataset - Azure Data Lake Storage Gen2 - DelimitedText - linkedservices(select created link services) - File path(creating a new filename-population_by_age_tsv) - first row as header - Import schema (none - we are not manipulating the data)

ds_population_raw_tsv

VALIDATE ALL TOP BAR

-------------------------------------------------------------------------------------------
--------PIPELINES---------------
Author(left bar, 2nd from the top) - Pipelines - new pipeline - name the pipeline - Settings(bottom portion) - concurrency(number of time pipeline should run) 

pl_ingest_population_data

Activities (tab) - drop down - copy data - general - name - description -  Timeout(0.00:10:00 - run for 10 mins then error) - retry - retry interval - Source(tab) - Source dataset - Sink(tab) - Sink dataset(target dataset) - Mapping(tab - to map different columns source to target) for that import schemas to map - validate the pipeline

Debug - to run the file



