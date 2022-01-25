Cleaning individual data with biologically implausible values in NCD-RisC database
==================================================================================

This document is the protocol for cleaning multiple variables in the
NCD-RisC database, which has the following steps:  

1.  Applying univariate plausibility ranges  
2.  Applying multivariate constraints  
3.  Multivariate outlier detection  

### 1. Univariate plausibility ranges

Data outside the following plausibility ranges will be removed.

*Anthropometrics*

<table>
<colgroup>
<col style="width: 9%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 11%" />
<col style="width: 10%" />
<col style="width: 9%" />
<col style="width: 17%" />
<col style="width: 19%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Variable</th>
<th style="text-align: left;">Height (cm)</th>
<th style="text-align: left;">Weight (kg)</th>
<th style="text-align: left;">BMI (kg/m2)</th>
<th style="text-align: left;">Waist (cm)</th>
<th style="text-align: left;">Hip (cm)</th>
<th style="text-align: left;">Waist-to-hip ratio</th>
<th style="text-align: left;">Waist-to-height ratio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">5-9 years</td>
<td style="text-align: left;">60-180</td>
<td style="text-align: left;">5-90</td>
<td style="text-align: left;">6-40</td>
<td style="text-align: left;">20-150</td>
<td style="text-align: left;">30-180</td>
<td style="text-align: left;">0.4-1.8</td>
<td style="text-align: left;">0.2-1.5</td>
</tr>
<tr class="even">
<td style="text-align: left;">10-14 years</td>
<td style="text-align: left;">80-200</td>
<td style="text-align: left;">8-150</td>
<td style="text-align: left;">8-60</td>
<td style="text-align: left;">20-200</td>
<td style="text-align: left;">30-200</td>
<td style="text-align: left;">0.4-1.8</td>
<td style="text-align: left;">0.2-1.5</td>
</tr>
<tr class="odd">
<td style="text-align: left;">15+ years</td>
<td style="text-align: left;">100-250</td>
<td style="text-align: left;">12-300</td>
<td style="text-align: left;">10-80</td>
<td style="text-align: left;">30-300</td>
<td style="text-align: left;">40-300</td>
<td style="text-align: left;">0.4-2.0</td>
<td style="text-align: left;">0.2-2.0</td>
</tr>
</tbody>
</table>

*Blood Pressure*

<table>
<thead>
<tr class="header">
<th style="text-align: left;">Variable</th>
<th style="text-align: left;">SBP (mmHg)</th>
<th style="text-align: left;">DBP (mmHg)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">All ages</td>
<td style="text-align: left;">70-270</td>
<td style="text-align: left;">30-150</td>
</tr>
</tbody>
</table>

*Lipids*

<table>
<thead>
<tr class="header">
<th style="text-align: left;">Variable</th>
<th style="text-align: left;">TC (mmol/L)</th>
<th style="text-align: left;">HDL (mmol/L)</th>
<th style="text-align: left;">LDL (mmol/L)</th>
<th style="text-align: left;">Triglycerides (mmol/L)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">All ages</td>
<td style="text-align: left;">1.75-20</td>
<td style="text-align: left;">0.5-10</td>
<td style="text-align: left;">0.4-5</td>
<td style="text-align: left;">0.2-20</td>
</tr>
</tbody>
</table>

*Glucose*

<table>
<thead>
<tr class="header">
<th style="text-align: left;">Variable</th>
<th style="text-align: left;">FPG (mmol/L)</th>
<th style="text-align: left;">OGTT (mmol/L)</th>
<th style="text-align: left;">HbA1c (%)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">All ages</td>
<td style="text-align: left;">2.5-30</td>
<td style="text-align: left;">1.5-30</td>
<td style="text-align: left;">3-18</td>
</tr>
</tbody>
</table>

*Kidney related variable*

<table>
<thead>
<tr class="header">
<th style="text-align: left;">Variable</th>
<th style="text-align: left;">Serum creatinine (µmol/L)</th>
<th style="text-align: left;">eGFR (mL/min/1.73m2)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">All ages</td>
<td style="text-align: left;">8-1800</td>
<td style="text-align: left;">5-250</td>
</tr>
</tbody>
</table>

### 2. Multivariate constraints

The following constraints are applied after removing data outside the
plausibility ranges listed above:  

-   SBP &gt; DBP  
-   TC &gt; LDL  
-   TC &gt; HDL  
-   TC – (LDL + HDL) ≤ margin of error\*

\*“margin of error” is determined by using the Cholesterol Reference
Method Laboratory Network permitted measurement error limits for TC
(8.9%), HDL (13%) and LDL (12%) as follows:  

-   Calculate errors in worst case scenario, i.e., TC underestimated and
    HDL/LDL overestimated, each by the largest error permitted;  
-   The limit of errors by quartiles of TC using US NHANES data:  

<table>
<thead>
<tr class="header">
<th style="text-align: left;">TC range (mmol/L)</th>
<th style="text-align: left;">&lt;4.040</th>
<th style="text-align: left;">4.040 to &lt;4.714</th>
<th style="text-align: left;">4.714 to &lt;5.465</th>
<th style="text-align: left;"><span class="math inline">≥</span> 5.465</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Margin of error (mmol/L)</td>
<td style="text-align: left;">-0.7125</td>
<td style="text-align: left;">-0.8821</td>
<td style="text-align: left;">-0.9700</td>
<td style="text-align: left;">-1.7520</td>
</tr>
</tbody>
</table>

### 3. Multivariate outlier detection

After applying both univariate plausibility ranges and multivariate
constraints, multivariate outlier detection is carried out on pairs of
variables within the same risk factor family (see lists later).  
In each pair, a method based on Mahalanobis distance
([1](#ref-filzmoser2004multivariate)) is used to calculate the distance
of the data points to the centre of all available data, and those that
lie outside a certain threshold will be removed. Although called
“outlier detection”, the threshold is chosen to catch only extreme
values that are implausible. The points detected and removed should be
examined in scatter plots.

#### Data Normalization

Mahalanobis outlier detection method assumes the data to be normally
distributed. We suggest to compare the distribution of each variable to
the variable log transformed, and pick the closest to normal
distribution. In case neither the variable nor it’s log transformation
are close to be normally distributed, alternative non-parametric methods
should be used.

#### Pairs of variables considered

All pairs of variables from the same family (anthropometrics, blood
pressure etc…) should be considered.  
For blood pressure, if multiple measurements are taken, the average SBP
and DBP are calculated before multivariate cleaning, and after excluding
measurements outside of plausibility ranges, by discarding the first
measurement and averaging the remainings.  
For lipids, LDL (or non-HDL) is very skewed,so we advise to not clean on
the pair LDL-TC using mahalanobis distance.  
Glucose variables tend to have a very skewed distribution and we advise
to not clean any pair of glucose variables using Mahalanobis distance.  
For Kidney, eGFR is calculated from serum creatinine using a
regression-based model (eg. CKD-EPI) hence multivariate cleaning is not
needed.

#### Procedure of multivariate outlier detection

For each pair listed above:  
- Compute the Mahalanobis of distance of all the data points after
normalisation  
- Exclude points with distance larger than 40.08 (quantile of chi2
distribution equivalent to 6SD for normal distribution)  

#### Code and example

For the code and an example on simulated data of the multivariate
outlier detection procedure go to:
<a href="https://github.com/NCD-RisC/Multivariate-cleaning" class="uri">https://github.com/NCD-RisC/Multivariate-cleaning</a>

**References:**

1. Filzmoser P, Reimann C, Garrett R. A multivariate outlier detection
method. Citeseer; 2004.
