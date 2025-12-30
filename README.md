# CSTR-Temperature-Anomaly-Detection-with-Rolling-3-Rule
This is an easy level data science project where the trio-numpy, pandas and matplotlib are used to first simulate a dataset assuming normal distribution, then anomalies are injected and later detected and analyzed via plots. Is a must look for all data enthusiasts in their initial years.

CSTR Temperature Anomaly Detection with Rolling 3σ Rule

Objective:-
    Simulated a min-by-min data for 24 hours for T of a CSTR with gaussian noise and injected fault periods within it.
    Detect the anomolies in the data using rolling mean and 3σ rule and show it via plots
Following is a part by part description of what is done in the project.
    
  A.Data generation:
    -Generated time intervals pandas series using pd.date_range(start,stop,periods,freq)
    -Sampling over 24 hours(1440 points in total) usin np.random.normal(loc,scale,size)
    -Generated a pandas dataframe by inculcating both the series above to frame the base data and did Exploratory Data Analysis for it.
    
  B.Error Injection
    -Two types of errors were injected into the dataframe:-
        1.Missing values/NaN
        2.Outliers

  C.Pre‑processing:
    -Interpolated the data to fill spaces using df.interpolate(method='time') to fill NaN values
    -Used window and df.rolling(window,min_periods).mean() to find out the rolling mean and std and calculated deviation.

  D.Detection logic:
    -Deviation T_dev = T_reactor-T_roll_mean computed for each timestamp
    -Point is classified as an outlier if T_dev>T_roll_sigma

  E.Results:
    -Precision: 0.86
    -Recall: 0.10
    -Outlier rate: 0.49%
    -Fraction of fault points detected: 0.10

  F.Limitations:
    -The rolling 3σ method is effective at catching sudden transitions but less sensitive to slow drifts or sustained plateaus once the mean adapts.

Learnings:- Three important things to carry on:-
    a.Time series mindset- Never assume time to be just another column, its more than that in reality. Use a proper time index and time aware operations.
    Time aware operations include rolling,windowed stats etc..

.    b.CLeaning assumptions:- The choice of wether to drop or fill the data using one of the options depends not only on the data scientist's comfortability 
    but more on the process. Here the temperature variable tends to be continuous in nature and hence interpolation is a good choice.

.    c.Anomolies and Evaluation:-Labelling synthetic “true_fault” vs “is_outlier” and computing precision/recall is exactly how to evaluate an anomaly detector.
