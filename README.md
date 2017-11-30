# CDC WONDER API - Detailed Mortality Reference

<p><img src="https://www.cdc.gov/TemplatePackage/3.0/images/homepage/masthead.svg" alt="" width="671" height="90" /></p>
<p><a href="https://wonder.cdc.gov/" target="_blank">CDC WONDER</a> is a query tool from the Centers for Disease Control (CDC) that provides access to a collection of online databases for the analysis of public health data.</p>
<p>The following are a sampling of databases available through WONDER that provide vital statistics data through CDC's National Center for Health Statistics</p>
<ul>
<li><a href="https://wonder.cdc.gov/natality.html" target="_blank">Births</a></li>
<li><a href="https://wonder.cdc.gov/ucd-icd10.html" target="_blank">Detailed Mortality</a></li>
<li><a href="https://wonder.cdc.gov/mortSQL.html" target="_blank">Compressed Mortality</a></li>
<li><a href="https://wonder.cdc.gov/mcd.html" target="_blank">Multiple cause of death</a></li>
<li><a href="https://wonder.cdc.gov/lbd.html" target="_blank">Infant Deaths</a></li>
</ul>
<p>For this example, we will focus on the <strong>Detailed Mortality</strong> database, which provides number of deaths and death rates (crude or age-adjusted) for underlying cause of death at the national level (state and county restricted through API). Using the query tool, the user can select grouping and filtering variables that are used to generate a dataset. <span style="color: #ff0000;"><strong>Results from the endpoint include a&nbsp;data table along with applicable footnotes and caveats</strong></span>, which can then be exported to a tab delimited file or visualized.</p>
<p>WONDER provides an API that allows the same queries to be issued through a <span style="color: #ff0000;"><strong>HTTP POST request</strong></span> to WONDER's web server (<span style="color: #ff0000;"><strong>no authentication required</strong></span>). Requests and responses are issued in XML format and are detailed in the <a href="https://wonder.cdc.gov/wonder/help/WONDER-API.html" target="_blank">API Documentation</a> page. The documentation specifies that when running an automated query, the a limit of one query for every 2 minutes should be made to allow for good system recovery time.</p>
<p>Each XML request consists of a series of parameter tags with name and value children in the following format:</p>
<pre><code>&lt;request-parameters&gt;
    &lt;parameter&gt;
        &lt;name&gt;&lt;/name&gt;
        &lt;value&gt;&lt;/value&gt;
    &lt;parameter&gt;
    ...
&lt;/request-parameters&gt;</code></pre>
<p>For <strong><span style="color: #ff0000;">examples of the format for the request and response</span></strong>, see the <a href="#exampleXML" target="">Example Request and Response</a>&nbsp;section for detailed examples.</p>
<p>Available parameter names and values vary by database in WONDER. The <a href="https://wonder.cdc.gov/wonder/help/WONDER-API.html" target="_blank">WONDER API Documentation</a> recommends viewing the HTML source for the web form in the query tool to access available parameter names and values. For convenience, parameter names and values are provided below.</p>
<p>&nbsp;</p>
<h2><a id="exampleXML"></a>Example XML Request and Response</h2>
<ol>
<li>U.S. national cancer deaths (ICD-10 codes C00-D48) by year and by race, for the 5 year time period 2009-2013. Number of deaths, population estimates, crude death rates and age-adjusted death rates per 100,000 persons, 95% confidence intervals and standard errors for age-adjusted death rates.
<ul>
<li><a href="https://wonder.cdc.gov/wonder/help/API-Examples/D76_Example1-req.xml" target="_blank">Example 1 Request</a></li>
<li><a href="https://wonder.cdc.gov/wonder/help/API-Examples/D76_Example1-resp.xml" target="_blank">Example 1 Response</a></li>
</ul>
</li>
<li>U.S. national injury deaths for persons age 18 and under, by Injury Intent and Injury Mechanism, for years 1999-2013. Number of deaths, population estimates, crude death rates.
<ul>
<li><a href="https://wonder.cdc.gov/wonder/help/API-Examples/D76_Example2-req.xml" target="_blank">Example 2 Request</a></li>
<li><a href="https://wonder.cdc.gov/wonder/help/API-Examples/D76_Example2-resp.xml" target="_blank">Example 2 Response</a></li>
</ul>
</li>
</ol>
<p>&nbsp;</p>
<h2><a id="creatingRequest"></a>Example Python Scripts</h2>
<p>For Python examples of creating, sending, and processing a request, as well as running some basic visualizations, see <a href="https://github.com/alipphardt/cdc-wonder-api/blob/master/CDC%2BWONDER%2BAPI%2BExample.ipynb">https://github.com/alipphardt/cdc-wonder-api/blob/master/CDC%2BWONDER%2BAPI%2BExample.ipynb</a></p>
<p>&nbsp;</p>

<h2><a id="referenceParameters"></a>Reference for All Request Parameters</h2>
<ul>
<li><a href="#bParams" target="">B - Group By Parameters</a></li>
<li><a href="#mParams" target="">M - Measure Parameters</a></li>
<li><a href="#fivParams" target="">F/I/V Parameters</a></li>
<li><a href="#oParams" target="">O - Other Parameters</a></li>
<li><a href="#vmParams" target="">VM - Values for non-standard age adjusted rates</a></li>
<li><a href="#vParams" target="">V - Variable Values</a></li>
<li><a href="#miscParams" target="">Miscellaneous Parameters</a></li>
</ul>
<p>&nbsp;</p>
<h3 id="B---Group-By-Parameters"><a id="bParams"></a>B - Group By Parameters</h3>
<p>Parameter Names:</p>
<ul>
<li>B_1</li>
<li>B_2</li>
<li>B_3</li>
<li>B_4</li>
<li>B_5</li>
</ul>
<p>The following is a listing of available values for each parameter name in the format:</p>
<p><code>&lt;value&gt; - &lt;description&gt;</code></p>
<h5>Location</h5>
<ul>
<li>D76.V10-level1 - Census Region</li>
<li>D76.V10-level2 - Census Division</li>
<li>D76.V27-level1 - HHS Region</li>
<li>D76.V9-level1 - State</li>
<li>D76.V9-level2 - County</li>
<li>D76.V19 - 2013 Urbanization</li>
<li>D76.V11 - 2006 Urbanization</li>
</ul>
<h5 id="Demographics">Demographics</h5>
<ul>
<li>D76.V5 - Age Groups</li>
<li>D76.V7 - Gender</li>
<li>D76.V17 - Hispanic Origin</li>
<li>D76.V8 - Race</li>
</ul>
<h5 id="Year-and-Month">Year and Month</h5>
<ul>
<li>D76.V1-level1 - Year</li>
<li>D76.V1-level2 - Month</li>
</ul>
<h5 id="Weekday,-Autopsy,-Place-of-Death">Weekday, Autopsy, Place of Death</h5>
<ul>
<li>D76.V24 - Weekday</li>
<li>D76.V20 - Autopsy</li>
<li>D76.V21 - Place of Death</li>
</ul>
<h5 id="Cause-of-Death">Cause of Death</h5>
<ul>
<li>D76.V28 - 15 Leading Causes of Death</li>
<li>D76.V29 - 15 Leading Causes of Death (Infants)</li>
<li>D76.V2-level1 ICD - Chapter</li>
<li>D76.V2-level2 ICD - Sub-Chapter</li>
<li>D76.V2-level3 - Cause of death</li>
<li>D76.V4 - ICD-10 113 Cause List</li>
<li>D76.V12 - ICD-10 130 Cause List (Infants)</li>
<li>D76.V22 - Injury Intent</li>
<li>D76.V23 - Injury Mechanism &amp; All Other Leading Causes</li>
<li>D76.V25 - Drug/Alcohol Induced Causes</li>
</ul>
<p>&nbsp;</p>

<h3 id="M---Measure-Parameters"><a id="mParams"></a>M - Measure Parameters</h3>
<p>Deaths, Population and Crude Rate are included by default. Additional measures may be added and are included below:</p>
<p><code>&lt;name&gt; - &lt;value&gt; - &lt;description&gt;</code></p>
<ul>
<li>M_1 - D76.M1 - Deaths</li>
<li>M_2 - D76.M2 - Population</li>
<li>M_3 - D76.M3 - Crude Rate</li>
<li>M_31 - D76.M31 - Crude Rate Standard Error</li>
<li>M_32 - D76.M32 - Crude 95% Confidence Interval</li>
<li>M_4 - D76.M4 - Age-adjusted Rate</li>
<li>M_41 - D76.M41 - Age-adjusted Rate Standard Error</li>
<li>M_42 - D76.M42 - Age-adjusted Rate Confidence Interval</li>
<li>M_9 - D76.M9 - Percent of Total Deaths</li>
</ul>
<p>&nbsp;</p>

<h3><a id="fivParams"></a>F/I/V Parameters</h3>
<p>The <em>Detailed Mortality</em> database contains several variables that may take on one or more values and may be modified by F/I/V parameters</p>
<ul>
<li>D76.V1 - Year and Month</li>
<li>D76.V10 - Census Regions</li>
<li>D76.V2 - ICD-10 Codes</li>
<li>D76.V27 - HHS Regions</li>
<li>D76.V9 - States and Counties</li>
</ul>
<h5>D76.V1 - Year and Month</h5>
<p>Available years in the <strong>Detailed Mortality</strong> database run from 1999 through 2015. Values for F/I/V parameters (F_D76.V1, I_D76.V1, V_D76.V1) follow this format:</p>
<ul>
<li>F - <code>&lt;year1&gt; &lt;year2&gt;</code>
<ul>
<li>Example: "2009 2010"</li>
</ul>
</li>
<li>I - <code>&lt;year&gt; (&lt;year&gt;)</code>
<ul>
<li>Example: "2009 (2009) 2010 (2010)"</li>
</ul>
</li>
<li>V - <code>&lt;year&gt; (&lt;year&gt;)</code>
<ul>
<li>Example: "2009 (2009) 2010 (2010)"</li>
</ul>
</li>
</ul>
<p>With month included, the following format is used (Month names map to two digit codes)</p>
<ul>
<li>F - <code>&lt;year1&gt;/&lt;month1&gt; &lt;year2&gt;/&lt;month2&gt;</code>
<ul>
<li>Example: "2009/01 2009/02"</li>
</ul>
</li>
<li>I - <code>&lt;year1&gt;/&lt;month1&gt; (&lt;month1 abbrev&gt;., &lt;year 1&gt;) &lt;year2&gt;/&lt;month2&gt; (&lt;month2 abbrev&gt;., &lt;year 2&gt;)</code>
<ul>
<li>Example: "2009/01 (Jan., 2009) 2010/02 (Feb., 2010)"</li>
</ul>
</li>
<li>V - <code>&lt;year1&gt;/&lt;month1&gt; (&lt;month1 abbrev&gt;., &lt;year 1&gt;) &lt;year2&gt;/&lt;month2&gt; (&lt;month2 abbrev&gt;., &lt;year 2&gt;)</code>
<ul>
<li>Example: "2009/01 (Jan., 2009) 2010/02 (Feb., 2010)"</li>
</ul>
</li>
</ul>
<p>To include all dates:</p>
<ul>
<li>F - <code>*All*</code></li>
<li>I - <code>*All* (All Dates)</code></li>
<li>V - <code>*All* (All Dates)</code></li>
</ul>
<h5 id="D76.V10---Census-Regions">D76.V10 - Census Regions</h5>
<p>In keeping with the vital statistics policy for public data sharing, only national data are available for query by the API. Queries for mortality and births statistics from the National Vital Statistics System cannot limit or group results by any location field, such as Region, Division, State or County, or Urbanization (urbanization categories map to specific geographic counties).</p>
<ul>
<li>F_D76.V10 - "<code>*All*</code>"</li>
<li>I_D76.V10 - "<code>*All* (The United States)</code>"</li>
<li>V_D76.V10 - ""</li>
</ul>
<h5 id="D76.V2---ICD-10-Codes">D76.V2 - ICD-10 Codes</h5>
<ul>
<li>*All* - *All* (All Causes of Death)</li>
<li>A00-B99 - A00-B99 (Certain infectious and parasitic diseases)</li>
<li>C00-D48 - C00-D48 (Neoplasms)</li>
<li>D50-D89 - D50-D89 (Diseases of the blood and blood-forming organs and certain disorders involving the immune mechanism)</li>
<li>E00-E88 - E00-E88 (Endocrine, nutritional and metabolic diseases)</li>
<li>F01-F99 - F01-F99 (Mental and behavioural disorders)</li>
<li>G00-G98 - G00-G98 (Diseases of the nervous system)</li>
<li>H00-H57 - H00-H57 (Diseases of the eye and adnexa)</li>
<li>H60-H93 - H60-H93 (Diseases of the ear and mastoid process)</li>
<li>I00-I99 - I00-I99 (Diseases of the circulatory system)</li>
<li>J00-J98 - J00-J98 (Diseases of the respiratory system)</li>
<li>K00-K92 - K00-K92 (Diseases of the digestive system)</li>
<li>L00-L98 - L00-L98 (Diseases of the skin and subcutaneous tissue)</li>
<li>M00-M99 - M00-M99 (Diseases of the musculoskeletal system and connective tissue)</li>
<li>N00-N98 - N00-N98 (Diseases of the genitourinary system)</li>
<li>O00-O99 - O00-O99 (Pregnancy, childbirth and the puerperium)</li>
<li>P00-P96 - P00-P96 (Certain conditions originating in the perinatal period)</li>
<li>Q00-Q99 - Q00-Q99 (Congenital malformations, deformations and chromosomal abnormalities)</li>
<li>R00-R99 - R00-R99 (Symptoms, signs and abnormal clinical and laboratory findings, not elsewhere classified)</li>
<li>U00-U99 - U00-U99 (Codes for special purposes)</li>
<li>V01-Y89 - V01-Y89 (External causes of morbidity and mortality)</li>
</ul>
<h5 id="D76.V27---HHS-Regions">D76.V27 - HHS Regions</h5>
<p>In keeping with the vital statistics policy for public data sharing, only national data are available for query by the API. Queries for mortality and births statistics from the National Vital Statistics System cannot limit or group results by any location field, such as Region, Division, State or County, or Urbanization (urbanization categories map to specific geographic counties).</p>
<ul>
<li>F_D76.V27 - "<code>*All*</code>"</li>
<li>I_D76.V27 - "<code>*All* (The United States)</code>"</li>
<li>V_D76.V27 - ""</li>
</ul>
<h5 id="D76.V9---State-and-County-Codes">D76.V9 - State and County Codes</h5>
<p>In keeping with the vital statistics policy for public data sharing, only national data are available for query by the API. Queries for mortality and births statistics from the National Vital Statistics System cannot limit or group results by any location field, such as Region, Division, State or County, or Urbanization (urbanization categories map to specific geographic counties).</p>
<ul>
<li>F_D76.V9 - "<code>*All*</code>"</li>
<li>I_D76.V9 - "<code>*All* (The United States)</code>"</li>
<li>V_D76.V9 - ""</li>
</ul>
<h3>&nbsp;</h3>
<h3 id="O---Other-Parameters"><a id="oParams"></a>O - Other Parameters</h3>
<ul>
<li>O_V10<em>fmode - Controls whether Census Regions pulls from regular (F</em>) or advanced finder (V_) parameters
<ul>
<li>freg | fadv</li>
</ul>
</li>
<li>O_V1<em>fmode - Controls whether Year and Month pulls from regular (F</em>) or advanced finder (V_) parameters
<ul>
<li>freg | fadv</li>
</ul>
</li>
<li>O_V27<em>fmode - Controls whether HHS Regions pulls from regular (F</em>) or advanced finder (V_) parameters
<ul>
<li>freg | fadv</li>
</ul>
</li>
<li>O_V2<em>fmode - Controls whether ICD Code pulls from regular (F</em>) or advanced finder (V_) parameters
<ul>
<li>freg | fadv</li>
</ul>
</li>
<li>O_V9<em>fmode - Controls whether State/County pulls from regular (F</em>) or advanced finder (V_) parameters
<ul>
<li>freg | fadv</li>
</ul>
</li>
<li>O_aar
<ul>
<li>aar_none | aar_std | aar_nonstd</li>
</ul>
</li>
<li>O_aar_enable - Enable Age Adjusted Rate options. Set to true to allow for confidence interval and standard error options
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_aar_CI - age adjusted rate 95% confidence interval
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_aar_SE - age adjusted rate standard error
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_age
<ul>
<li>D76.V5 - Ten-Year Age Groups</li>
<li>D76.V51 - Five-Year Age Groups</li>
<li>D76.V52 - Single-Year Age Groups</li>
<li>D76.V6 - Infant Age Groups</li>
</ul>
</li>
<li>O_title - description to display as a title with your results.</li>
<li>O_rate_per - calculate rates per X people
<ul>
<li>1000 | 10000 | 100000 | 1000000</li>
</ul>
</li>
<li>O_post_pops - Use archive rates (calculated with postcensal populations for 2001-2009)
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_aar_nonstd - Use non-standard rates. If true, supply values for VM variables
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_aar_pop - The year "2000 U.S. standard" is the default population selection for the calculation of age-adjusted rates. However, you can select other standard populations, or select specific population criteria to determine the age distribution ratios.
<ul>
<li>0000 - 2000 U.S. Std Population</li>
<li>1940 - 1940 U.S. Std Million</li>
<li>1970 - 1970 U.S. Std Million</li>
<li>2000 - 2000 U.S. Std Million</li>
</ul>
</li>
<li>O_location -
<ul>
<li>D76.V9 - States</li>
<li>D76.V10 - Census Regions</li>
<li>D76.V27 - HHS Regions</li>
</ul>
</li>
<li>O_javascript - Turn on if javascript is enabled. Default is off
<ul>
<li>off | on</li>
</ul>
</li>
<li>O_ucd - set which field to use for underlying cause of death
<ul>
<li>D76.V2 - ICD-10 Codes</li>
<li>D76.V12 - ICD-10 130 Cause List (Infants)</li>
<li>D76.V25 - Drug/Alcohol Induced Causes</li>
<li>D76.V4 - ICD-10 113 Cause List</li>
<li>D76.V22 - Injury Intent and Mechanism</li>
</ul>
</li>
<li>O_urban
<ul>
<li>D76.V19 - 2013 Urbanization</li>
<li>D76.V11 - 2006 Urbanization</li>
</ul>
</li>
<li>O_show_totals - show totals
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_show_zeros - show zero values
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_show_suppressed - show suppressed values
<ul>
<li>true | false</li>
</ul>
</li>
<li>O_precision - number of decimal places
<ul>
<li><code>&lt;number between 0 and 9, inclusive&gt;</code></li>
</ul>
</li>
<li>O_timeout - data access timeout in minutes
<ul>
<li>60 - 1 minute</li>
<li>120 - 2 minutes</li>
<li>180 - 3 minutes</li>
<li>240 - 4 minutes</li>
<li>300 - 5 minutes</li>
<li>360 - 6 minutes</li>
<li>420 - 7 minutes</li>
<li>480 - 8 minutes</li>
<li>540 - 9 minutes</li>
<li>600 - 10 minutes</li>
<li>660 - 11 minutes</li>
<li>720 - 12 minutes</li>
<li>780 - 13 minutes</li>
<li>840 - 14 minutes</li>
<li>900 - 15 minutes</li>
</ul>
</li>
</ul>
<h3>&nbsp;</h3>
<h3 id="VM---Values-for-non-standard-age-adjusted-rates"><a id="vmParams"></a>VM - Values for non-standard age adjusted rates</h3>
<ul>
<li>Year - VM_D76.M6_D76.V1_S - <em>All</em> | list of years from 1999-2015 (inclusive)</li>
<li>Gender - VM_D76.M6_D76.V7
<ul>
<li>F - Female</li>
<li>M - Male</li>
</ul>
</li>
<li>Hispanic Origin - VM_D76.M6_D76.V17
<ul>
<li>*All* - All Origins</li>
<li>2135-2 - Hispanic or Latino</li>
<li>2186-2 - Not Hispanic or Latino</li>
<li>NS - Not Stated</li>
</ul>
</li>
<li>Race - VM_D76.M6_D76.V8
<ul>
<li>*All* - All Races</li>
<li>1002-5 - American Indian or Alaska Native</li>
<li>A-PI - Asian or Pacific Islander</li>
<li>2054-5 - Black or African American</li>
<li>2106-3 - White</li>
</ul>
</li>
<li>Location - VM_D76.M6_D76.V10</li>
</ul>
<h3>&nbsp;</h3>
<h3 id="V---Variable-Values"><a id="vParams"></a>V - Variable Values</h3>
<p>Variable values to limit in the "where" clause of the query, found in multiple select list boxes and advanced finder text entry boxes in the "Request Form."</p>
<ul>
<li>V_D76.V19 - 2013 Urbanization
<ul>
<li>*All* - All Categories</li>
<li>1 - Large Central Metro</li>
<li>2 - Large Fringe Metro</li>
<li>3 - Medium Metro</li>
<li>4 - Small Metro</li>
<li>5 - Micropolitan (non-metro)</li>
<li>6 - NonCore (non-metro)</li>
</ul>
</li>
<li>V_D76.V11 - 2006 Urbanization
<ul>
<li>*All* - All Categories</li>
<li>1 - Large Central Metro</li>
<li>2 - Large Fringe Metro</li>
<li>3 - Medium Metro</li>
<li>4 - Small Metro</li>
<li>5 - Micropolitan (non-metro)</li>
<li>6 - NonCore (non-metro)</li>
</ul>
</li>
<li>V_D76.V5 - Ten-Year Age Groups
<ul>
<li>*All* - All Ages</li>
<li>1 - &lt; 1 year</li>
<li>1-4 - 1-4 years</li>
<li>5-14 - 5-14 years</li>
<li>15-24 - 15-24 years</li>
<li>25-34 - 25-34 years</li>
<li>35-44 - 35-44 years</li>
<li>45-54 - 45-54 years</li>
<li>55-64 - 55-64 years</li>
<li>65-74 - 65-74 years</li>
<li>75-84 - 75-84 years</li>
<li>85+ - 85+ years</li>
<li>NS - Not Stated</li>
</ul>
</li>
<li>V_D76.V51 - Five-Year Age Groups
<ul>
<li>*All* - All Ages</li>
<li>1 - &lt; 1 year</li>
<li>1-4 - 1-4 years</li>
<li>5-9 - 5-9 years</li>
<li>10-14 - 10-14 years</li>
<li>15-19 - 15-19 years</li>
<li>20-24 - 20-24 years</li>
<li>25-29 - 25-29 years</li>
<li>30-34 - 30-34 years</li>
<li>35-39 - 35-39 years</li>
<li>40-44 - 40-44 years</li>
<li>45-49 - 45-49 years</li>
<li>50-54 - 50-54 years</li>
<li>55-59 - 55-59 years</li>
<li>60-64 - 60-64 years</li>
<li>65-69 - 65-69 years</li>
<li>70-74 - 70-74 years</li>
<li>75-79 - 75-79 years</li>
<li>80-84 - 80-84 years</li>
<li>85-89 - 85-89 years</li>
<li>90-94 - 90-94 years</li>
<li>95-99 - 95-99 years</li>
<li>100+ - 100+ years</li>
<li>NS - Not Stated</li>
</ul>
</li>
<li>V_D76.V52 - Single-Year Age Groups
<ul>
<li>0 - &lt; 1 year</li>
<li><code>&lt;Number between 1 and 99&gt;</code></li>
<li>100 - 100+ years</li>
<li>NS - Not Stated</li>
</ul>
</li>
<li>V_D76.V6 - Infant Age Groups
<ul>
<li>00 - All Infant Ages</li>
<li>1d - &lt; 1 day</li>
<li>1-6d - 1-6 days</li>
<li>7-27d - 7-27 days</li>
<li>28-364d - 28-364 days</li>
</ul>
</li>
<li>V_D76.V7 - Gender
<ul>
<li>F - Female</li>
<li>M - Male</li>
</ul>
</li>
<li>V_D76.V17 - Hispanic Origin
<ul>
<li>*All* - All Origins</li>
<li>2135-2 - Hispanic or Latino</li>
<li>2186-2 - Not Hispanic or Latino</li>
<li>NS - Not Stated</li>
</ul>
</li>
<li>V_D76.V8 - Race
<ul>
<li>*All* - All Races</li>
<li>1002-5 - American Indian or Alaska Native</li>
<li>A-PI - Asian or Pacific Islander</li>
<li>2054-5 - Black or African American</li>
<li>2106-3 - White</li>
</ul>
</li>
<li>V_D76.V24 - Weekday
<ul>
<li>*All* - All Weekdays</li>
<li>1 - Sunday</li>
<li>2 - Monday</li>
<li>3 - Tuesday</li>
<li>4 - Wednesday</li>
<li>5 - Thursday</li>
<li>6 - Friday</li>
<li>7 - Saturday</li>
<li>9 - Unknown</li>
</ul>
</li>
<li>V_D76.V20 - Autopsy
<ul>
<li>*All* - All Values</li>
<li>N - No</li>
<li>Y - Yes</li>
<li>U - Unknown</li>
</ul>
</li>
<li>V_D76.V21 - Place of Death
<ul>
<li>*All* - All Places</li>
<li>1 - Medical Facility - Inpatient</li>
<li>2 - Medical Facility - Outpatient or ER</li>
<li>3 - Medical Facility - Dead on Arrival</li>
<li>10 - Medical Facility - Status unknown</li>
<li>4 - Decedent's home</li>
<li>5 - Hospice facility</li>
<li>6 - Nursing home/long term care</li>
<li>7 - Other</li>
<li>9 - Place of death unknown</li>
</ul>
</li>
</ul>
<h3>&nbsp;</h3>
<h3><a id="miscParams"></a>Miscellaneous Parameters</h3>
<p>The following parameters should be included using the below name/value pairs.</p>
<ul>
<li>action-Send - Send</li>
<li>finder-stage-D76.V1 - codeset</li>
<li>finder-stage-D76.V1 - codeset</li>
<li>finder-stage-D76.V2 - codeset</li>
<li>finder-stage-D76.V27 - codeset</li>
<li>finder-stage-D76.V9 - codeset</li>
<li>stage - request</li>
</ul>
<p>&nbsp;</p>
