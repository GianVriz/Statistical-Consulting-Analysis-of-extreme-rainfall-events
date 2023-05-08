# Statistical Consulting: Analysis of extreme rainfall events

In the majority of the analyses regarding rainfall data, two types of available data exist:
* gauge data from stations (more accurate).
* weather radar data for pixels (available worldwide).  

Extreme daily precipitation refers to an amount of precipitation that is significantly higher than the average quantity of precipitation for a particular location and time period.
Extreme value theory (EVT) is a branch of statistics that deals with the study of very large or very small values, which are also commonly referred to as outliers or extremes.

Peak over threshold (POT) is a statistical method used to analyze extreme rainfall events. It involves identifying those rain events that exceed a certain threshold and analyzing the peaks of the excess rainfall. The threshold is typically set at a relatively high level to ensure that only a few number of events are analyzed. By analyzing the peaks of excess rainfall, it is possible to estimate the distribution of extreme rainfall and the likelihood of future events exceeding certain thresholds.

The main aims of the proposed project are the following:
* Extrapolation: using statistical methods to estimate missing values or extend the data to areas without any gauges.
* Systematic biases: integrate weather radar and rain gauge information to reduce random errors.

Following [Marra, et al. (2019)](https://www.sciencedirect.com/science/article/abs/pii/S0309170818309011), the two-parameter Weibull distribution is used to model the right tail of ordinary events (values $> 0.1$ mm).
    
$\mathbb{F}(x;\lambda,\kappa)=1-e^{-{(x/\lambda)}^\kappa}$,
where:
* $\lambda$ is a scale parameter. Larger values are associated with a larger magnitude of average events.
* $\kappa$ is a shape parameter. Greater values are associated with a faster decrease, i.e. light tail.

Using the global daily precipitation dataset created by
[Marra, Amponsah, and
Papalexiou (2023)](https://www.sciencedirect.com/science/article/abs/pii/S0309170823000234) and the satellite data available in [CMORPH Climate Data Record (CDR)](https://www.ncei.noaa.gov/products/climate-data-records/precipitation-cmorph), the parameters of the Weibull distribution are computed by applying both Maximum Likelihood Estimation (MLE) and Least Square (LS) regression in Weibull-transformed coordinates. If we limit the analysis to a single year (2018, i.e. the most recent one), for estimating the parameters of the Weibull distribution may be better using LS. However, if we broaden the timeframe (aggregated data between 2000-2018) to obtain a larger sample size, MLE is superior to LS.

Splitting the gauge data in training and test set, specific statistical tools are performed to study extrapolation's accuracy. XGboost turned out to be the best model to use for extending the data to areas without any gauges. However, while satellite data can aid in estimating data in gauge-free areas, they are not comprehensive enough to provide an acceptable depiction. A jointly analysis considering both satellite data and [Bioclimatic variables](https://worldclim.org/) increase the accuracy of the estimates. Thus, studying the existence of possible interconnections between the parameters of the Weibull distribution and Bioclimatic variables will be a crucial direction to improve extrapolation of extreme rainfall events.

<p align="center">
<img src="https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/blob/main/Slides/Wet_days_satellite_2008_2018.png" alt="drawing" width="300"/>   <img src="https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/blob/main/Slides/Wet_station_2000_2018.png" alt="drawing" width="300"/>
<p>

The repository includes the following folders:
* *[Satellite data](https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/tree/main/Satellite%20data)* \
  It contains files related to satellite data we used.
* *[Station data](https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/tree/main/Station%20data)* \
  It contains files related to station data we used.
* *[Prepare data](https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/blob/main/Prepare%20data.ipynb)* \
  It contains files related to data cleaning and preparation.
* *[Estimates](https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/tree/main/Estimates)* \
  It contains files related to the estimated models.
* *[Code](https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/tree/main/Code)* \
  Code scripts in R.
* *[Slides](https://github.com/GianVriz/Statistical-Consulting-Analysis-of-extreme-rainfall-events/tree/main/Slides)* \
  Slides and figure of the presentation at the University of Padua.

## Authors
* Gian Luca Vriz - [GianVriz](https://github.com/GianVriz)
* Riccardo De Santis
* Mehwish Zaman

## References
* Marra, Francesco et al. (2019). “A simplified MEV formulation to model extremes emerging from multiple nonstationary underlying processes”. In: Advances in Water Resources 127, pp. 280–290.
* Fick, Stephen E. and Robert J. Hijmans (2017). “WorldClim 2: new 1-km spatial resolution climate surfaces for global land areas”. In: International Journal of Climatology 37.12, pp. 4302–4315.
* Poboikova, Ivana and Zuzana Sedliakova (2014). “Comparison of four methods for estimating the Weibull distribution parameters”. In: Applied mathematical sciences 8, pp. 4137–4149.
* Marra, Francesco, William Amponsah, and Simon Michael Papalexiou (2023). “Non-asymptotic Weibull tails explain the statistics of extreme daily precipitation”. In: Advances in Water Resources 173, p. 104388.
* Zhang, Zeguo, Emil V. Stanev, and Sebastian Grayek (2020). “Reconstruction of the Basin-Wide Sea-Level Variability in the North Sea Using Coastal Data and Generative Adversarial Networks”. In: Journal of Geophysical Research: Oceans 125.12, e2020JC016402.
