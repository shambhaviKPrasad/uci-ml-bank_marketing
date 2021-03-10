# uci-ml-bank_marketing-eda
EDA on bank marketing dataset from the UCI ML repository

Data set source:
[Moro et al., 2014] S. Moro, P. Cortez and P. Rita. A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, Elsevier, 62:22-31, June 2014
http://repositorium.sdum.uminho.pt/bitstream/1822/14838/1/MoroCortezLaureano_DMApproach4DirectMKT.pdf
https://archive.ics.uci.edu/ml/datasets/Bank+Marketing

Data description:
Input variables:
bank client data:
1 - age (numeric)
2 - job : type of job (categorical: "admin.","blue-collar","entrepreneur","housemaid","management","retired","self-employed","services","student","technician","unemployed","unknown")
3 - marital : marital status (categorical: "divorced","married","single","unknown"; note: "divorced" means divorced or widowed)
4 - education (categorical: "basic.4y","basic.6y","basic.9y","high.school","illiterate","professional.course","university.degree","unknown")
5 - default: has credit in default? (categorical: "no","yes","unknown")
6 - housing: has housing loan? (categorical: "no","yes","unknown")
7 - loan: has personal loan? (categorical: "no","yes","unknown")

related with the last contact of the current campaign:
8 - contact: contact communication type (categorical: "cellular","telephone")
9 - month: last contact month of year (categorical: "jan", "feb", "mar", ..., "nov", "dec")
10 - day_of_week: last contact day of the week (categorical: "mon","tue","wed","thu","fri")
11 - duration: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y="no"). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.

other attributes:
12 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
13 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
14 - previous: number of contacts performed before this campaign and for this client (numeric)
15 - poutcome: outcome of the previous marketing campaign (categorical: "failure","nonexistent","success")

social and economic context attributes
16 - emp.var.rate: employment variation rate - quarterly indicator (numeric)
 Employment rates are defined as a measure of the extent to which available labour resources (people available to work) are being used. They are calculated as the ratio of the employed to the working age population. Employed people are those aged 15 or over who report that they have worked in gainful employment for at least one hour in the previous week or who had a job but were absent from work during the reference week. The working age population refers to people aged 15 to 64. This indicator is seasonally adjusted and it is measured in terms of thousand persons aged 15 and over; and in numbers of employed persons aged 15 to 64 as a percentage of working age population.
 Ref: https://data.oecd.org/emp/employment-rate.htm

17 - cons.price.idx: consumer price index - monthly indicator (numeric)
 Meaning: The Consumer Price Index (CPI) is a measure of the average change over time in the prices paid by urban consumers for a market basket of consumer goods and services. When economists talk about rising inflation, they are usually referring to a rise in the Consumer Price Index, which tracks overall prices on the retail level.
Inflation can have a negative impact on fixed-income assets when it results in higher interest rates. Fixed-income instruments include bonds and certificates of deposit (CD) like term deposits. Prices of fixed-income assets move opposite to their yields. Inflation typically occurs during periods of economic strength and when prices for wages, merchandise, and commodities begin to increase.
 Ref: https://www.bls.gov/cpi/
This is a lagging indicator, means that it is calcuated after the economic activity is concluded. A lagging indicator is an observable or measurable factor that changes some time after the economic, financial, or business variable it is correlated with changes.
 Ref: https://www.investopedia.com/terms/l/laggingindicator.asp
Lagging indicators are economic models that confirm trends that are already happening. The unemployment rate, for example, goes up only after the jobs have already been lost. Leading indicators, on the other hand, are forecasting models that try to predict a future change in the economy.
 Ref: https://www.gobankingrates.com/money/economy/economy-explained-consumer-confidence-index-affect/
 Significance: a higher CPI indicates higher inflation, while a falling CPI indicates lower inflation, or even deflation.

18 - cons.conf.idx: consumer confidence index - monthly indicator (numeric)
 Meaning: This consumer confidence indicator provides an indication of future developments of households' consumption and saving, based upon answers regarding their expected financial situation, their sentiment about the general economic situation, unemployment and capability of savings. An indicator above 100 signals a boost in the consumers’ confidence towards the future economic situation, as a consequence of which they are less prone to save, and more inclined to spend money on major purchases in the next 12 months. Values below 100 indicate a pessimistic attitude towards future developments in the economy, possibly resulting in a tendency to save more and consume less.
 Ref: OECD (2021), Consumer confidence index (CCI) (indicator). doi: 10.1787/46434d78-en (Accessed on 06 March 2021)
 Significance: Many businesses make use of the consumer confidence index to structure their marketing and sales efforts based on the current findings of the research. Bankers and other lending institutions make use of consumer confidence reports of this nature to gauge lending activity and the potential for an upswing in loan defaults
 Ref: https://www.wisegeek.com/what-is-the-consumer-confidence-index.htm )

19 - euribor3m: euribor 3 month rate - daily indicator (numeric)
 Meaning : The Euro Interbank Offered Rate is a daily reference rate, published by the European Money Markets Institute, based on the averaged interest rates at which Eurozone banks offer to lend unsecured funds to other banks in the euro wholesale money market.
 Ref: emmi-benchmarks.eu
 The 3 month Euribor interest rate is the interest rate at which a selection of European banks lend one another funds denominated in euros whereby the loans have a maturity of 3 months. Alongside the 3 month Euribor interest rate we have another 14 Euribor interest rates with different maturities. The Euribor interest rates are the most important European interbank interest rates. When the Euribor interest rates rise or fall (substantially) there is a high likelihood that the interest rates on banking products such as mortgages, savings accounts and loans will also be adjusted.
 Ref: https://www.global-rates.com/en/interest-rates/euribor/euribor-interest-3-months.aspx
20 - nr.employed: number of employees - quarterly indicator (numeric)

Output variable (desired target):
21 - y - has the client subscribed a term deposit? (binary: "yes","no")
 Meaning: A term deposit is a fixed-term investment that includes the deposit of money into an account at a financial institution. It is a type of deposit account held at a financial institution where money is locked up for some set period of time. Term deposits are usually short-term deposits with maturities ranging from one month to a few years. Typically, term deposits offer higher interest rates than traditional liquid savings accounts, whereby customers can withdraw their money at any time.
 Relation with interest rate: In periods of rising interest rates, consumers are more likely to purchase term deposits since the increased cost of borrowing makes savings more attractive. Also, with higher market interest rates, the financial institution will need to offer the investor a higher rate of interest, so the investor also earns more.
When interest rates decrease, consumers are encouraged to borrow and spend more, thereby stimulating the economy. In a low interest rate environment, demand for term deposits can decrease since investors can typically find alternative investment vehicles  that pay a higher rate.
 Relation with inflation : Interest rates don't keep up with rising inflation. Unfortunately, term deposits do not keep up with inflation. The inflation rate is a measure of how much prices rise in a given year. If the rate on a term deposit is 2% and the inflation rate in the U.S. is 2.5%, theoretically, the customer is not earning enough to compensate for price increases in the economy.
 Ref: https://www.investopedia.com/terms/t/termdeposit.asp)

Missing Attribute Values: There are several missing values in some categorical attributes, all coded with the "unknown" label. These missing values can be treated as a possible class label or using deletion or imputation techniques.

Note: The data [was] collected from 2008 to 2013, thus including the effects of the recent financial crisis.
 Ref: http://repositorium.sdum.uminho.pt/bitstream/1822/30994/1/dss-v3.pdf
