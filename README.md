# What-drives-the-price-of-a-car-

## BLUF (Bottom line up front): 
This data set shows the best predictor of a used car's value is the model year and odometer. The correlation matrix reflects features such as fuel=diesel, type=pickup and drive=4wd highly correlated to the price of the car. Ridge regression resulted in the model with the lowest MSE.

Top positive and negative 10 correlations for auto dataset: <br/>
<br/>
year                  0.527981<br/>
transmission_other    0.301938<br/>
type_pickup           0.246402<br/>
fuel_diesel           0.216246<br/>
drive_4wd             0.204054<br/>
manufacturer_ram      0.176575<br/>
fuel_other            0.164609<br/>
type_truck            0.160465<br/>
condition_good        0.157013<br/>
type_other            0.118321<br/>
manufacturer_gmc      0.075276<br/>
type_coupe            0.068575<br/>
state_wa              0.065604<br/>
drive_rwd             0.062483

<br/>
odometer                  -0.503517<br/>
drive_fwd                 -0.285530<br/>
transmission_automatic    -0.248266<br/>
fuel_gas                  -0.244953<br/>
condition_excellent       -0.200407<br/>
type_sedan                -0.186524<br/>
manufacturer_honda        -0.130797<br/>
manufacturer_nissan       -0.104855<br/>
manufacturer_hyundai      -0.096522<br/>
type_no_data              -0.083719<br/>
manufacturer_kia          -0.080829<br/>
type_hatchback            -0.077644<br/>
type_SUV                  -0.077461<br/>
manufacturer_volkswagen   -0.069046<br/>
manufacturer_subaru       -0.069010<br/>

### Data prep: 

### Original DF:
18 columns of data.
<br/>
I removed columns of little value or those missing large amounts of data, such as VIN, ID, paint color, etc.<br/>

#### Price: I filtered the price to the IQR and also removed any entries lower than $5000.
#### Odometer: I filtered the odometer values with IQR and replaced nulls with the mean.
#### Conditon: Ordinal data
#### Fuel, Drive, Tranmission, Type and state: OHE
#### Manufacturer: Removed any manufacturers with <5000 entries, OHE
#### Year: I dropped cars older than 1990, these values were mostly outliers
#### Missing data: Finally I dropped any rows with missing price data, leaving 223,378 rows of data.

### Initial plotting: Please review the summary of data tab, this will show useful plots of this data.

### Features Importance:
I ran a random forest regression modeal on all the features in the dataframe with n=100 estimators to evaluate features importance for modeling.


Feature  Importance<br/>
year    0.367097<br/>
odometer    0.198409<br/>
drive    0.130477<br/>
manufacturer    0.076941<br/>
fuel    0.073303<br/>
type    0.069757<br/>
state    0.041798<br/>
condition    0.021955<br/>
transmission    0.020263<br/>
<br/>

### Modeling:<br/>
After defining my dataframes for testing, I completed the following models:<br/>

### Linear regression: 
Built a model using the top 10 features from features selection: ['year','odometer','transmission_other','drive_fwd','fuel_gas','type_pickup','transmission_automatic','fuel_diesel', 'drive_4wd','condition_excellent']<br/>
Train MSE:  72354603.32109658<br/>
Test MSE:  73092330.60734843<br/>

### Polynomial regression: 
Built a model using the top 10 features from features selection: ['year','odometer','transmission_other','drive_fwd','fuel_gas','type_pickup','transmission_automatic','fuel_diesel', 'drive_4wd','condition_excellent']<br/>
I found i=3 is optimal degress of polynomial<br/>
Train MSE:  50227300.581849806<br/>
Test MSE:  50971358.99088974<br/>

### Grid search for alpha and ridge regression:<br/>
Alpha=0.1<br/>
Train MSE:  47757356.46<br/>
Test MSE:  48601731.18<br/>

### Grid search for and lasso regression:<br/>
Train MSE:  88731669.29<br/>
Test MSE:  89704552.25<br/>
Top 6 features:	year	condition	fuel	odometer	transmission	drive<br/>



