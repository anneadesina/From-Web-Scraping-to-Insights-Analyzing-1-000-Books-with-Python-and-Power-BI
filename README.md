# From-Web-Scraping-to-Insights-Analyzing-1-000-Books-with-Python-and-Power-BI
How I turned an online book catalogue into a structured dataset and interactive dashboard using Python, exploratory data analysis, and Power BI.
## Introduction: Turning Website Data into Insights

The internet contains a huge amount of information, but much of it is presented in ways that make analysis difficult. Product listings, prices, ratings, and availability information are often displayed across multiple web pages rather than in a single structured dataset.

For a data analyst, the challenge is not simply finding information. It is learning how to collect it, prepare it for analysis, identify meaningful patterns, and communicate the results effectively.

This was the motivation behind my individual web scraping project.

I worked with [Books to Scrape](https://books.toscrape.com/index.html), a demonstration website designed for practising web scraping. My objective was to collect information about 1,000 books, clean and analyze the data using Python, and build an interactive Power BI dashboard to communicate the findings.

The project followed a practical data analytics workflow:

**Web Scraping → Data Cleaning → Exploratory Data Analysis → Data Visualization → Insights and Recommendations**

Rather than treating Python and Power BI as separate tasks, I used them as complementary tools within the same analytical process.

## Why I Chose Books to Scrape

I selected Books to Scrape because its catalogue provided a structured and accessible environment for practising web scraping.

Each book listing contained information such as its title, price, star rating, availability, product page, and cover image. The catalogue also spanned multiple pages, creating an opportunity to practise pagination rather than collecting information from a single webpage.

The dataset contained both numerical and categorical variables, making it suitable for several types of analysis.

For example, I could calculate the average price of books, compare prices across rating categories, examine the distribution of ratings, and investigate differences in average prices across catalogue pages.

The project also provided an opportunity to understand how information presented on a website could be transformed into a structured dataset suitable for analysis in Python and Power BI.

## Step 1: Collecting the Data with Python

The first stage involved extracting information from the website.

I used Python libraries to handle different parts of the scraping process:

- **Requests:** Retrieved the website's HTML content.
- **BeautifulSoup:** Parsed the HTML and located individual book listings.
- **Pandas:** Organized the extracted information into a DataFrame.
- **NumPy:** Supported numerical data operations.
- **Matplotlib:** Created visualizations during exploratory data analysis.

The initial website request returned an HTTP status code of 200, indicating that the request was successful.

After inspecting the page structure, I identified the HTML elements containing the book information and developed a function to extract the required fields.

Because the catalogue extended across multiple pages, I used pagination to navigate through the listings. This allowed the scraping process to continue until the required 1,000 records had been collected.

### What Data Did I Collect?

The final dataset contained 1,000 book records across 50 catalogue pages, with seven attributes: page number, book title, price, star rating, availability, product URL, and image URL.

These fields provided enough information to explore pricing patterns, compare ratings, and examine the availability of the collected books.

## Step 2: Cleaning the Data

Collecting data is only one part of the analytical process. The extracted information must also be prepared before meaningful calculations can be performed.

During this stage, I addressed several data preparation challenges.

### Converting Prices into Numerical Values

The book prices were initially extracted as text containing the pound symbol and an unwanted character associated with text encoding.

I removed the unwanted characters and converted the price values into floating-point numbers. This allowed me to calculate measures such as the mean, median, minimum, and maximum prices.

### Converting Ratings into Numbers

The website represented ratings as words, such as One, Two, Three, Four, and Five. For numerical analysis, I mapped these categories to values from 1 to 5:

- One = 1
- Two = 2
- Three = 3
- Four = 4
- Five = 5

This transformation made it possible to calculate the average rating, compare rating frequencies, and investigate the relationship between ratings and prices.

### Cleaning Availability Information

The availability text was extracted from the relevant HTML elements and normalized to make it easier to read and group. This enabled me to summarize the stock status of the collected books.

### Handling Product Links

Some website links were relative paths rather than complete URLs. I used Python's `urljoin()` function to construct full URLs for individual book pages and cover images.

### Managing Pagination Responsibly

The catalogue was spread across multiple pages, so the scraping process needed to navigate through the website systematically. I used the pagination links to retrieve subsequent pages and included a one-second pause between requests to reduce request frequency.

Finally, I organized the extracted fields into a DataFrame and exported the dataset to CSV and Excel formats for further use.

### What Challenges Did I Encounter?

The main challenges involved navigating multiple pages, converting text into numerical values, handling currency formatting, and constructing complete URLs.

Working through these challenges helped me understand that successful web scraping requires more than retrieving HTML. The extracted information must be transformed into a format that supports reliable analysis.

Although the dataset was structured successfully, additional validation checks for missing values, duplicate records, invalid prices, and unexpected rating values would further strengthen its data quality.

## Step 3: Exploring the Data with Python

With the data collected and prepared, I moved to exploratory data analysis (EDA).

The purpose of this stage was to understand the dataset before building the dashboard. I wanted to investigate the price distribution, identify the cheapest and most expensive books, examine the rating distribution, and determine whether prices and ratings appeared to be related.

### What Is the Typical Price of a Book?

The average book price was **£35.07**, while the median price was **£35.98**.

The average represents the sum of all book prices divided by the number of books, while the median represents the middle price when the prices are arranged in ascending order.

The two values were relatively close, providing a useful summary of the catalogue's central pricing level. However, neither measure tells the complete story. Examining the price distribution is also important because two datasets can have similar averages but very different ranges of prices.

### What Were the Cheapest and Most Expensive Books?

The analysis identified the following titles:

- **Least expensive:** *An Abundance of Katherines* — £10.00, with a five-star rating.
- **Most expensive:** *The Perfect Play (Play by Play #1)* — £59.99, with a three-star rating.

These results demonstrated how filtering and sorting could be used to identify individual records of interest. They also provided an early indication that a book's price did not necessarily correspond to its star rating.

### How Were Book Ratings Distributed?

The rating analysis revealed the following:

- **1 star:** 226 books (22.6%)
- **2 stars:** 196 books (19.6%)
- **3 stars:** 203 books (20.3%)
- **4 stars:** 179 books (17.9%)
- **5 stars:** 196 books (19.6%)

One-star books formed the largest group, while four-star books were the least represented. Overall, the books were distributed across all five rating categories rather than being concentrated in just one.

### Does a Higher Price Mean a Higher Rating?

The Pearson correlation coefficient between book price and rating was approximately **0.03**, indicating almost no linear relationship in the collected dataset.

When I compared average prices by rating, four-star books had the highest average price at **£36.09**, followed by five-star books at **£35.37**. One-star books had the lowest average price at **£34.56**.

The differences were relatively small, suggesting that price alone was not a reliable indicator of a book's rating.

### What About Availability?

All 1,000 collected records were marked as **In stock**. The average price for this group was £35.07.

Although the availability field was successfully extracted, the absence of other stock statuses limited the conclusions that could be drawn. There was no meaningful basis for comparing in-stock books with out-of-stock books.

This highlighted an important analytical lesson: collecting a variable does not automatically mean the dataset contains enough variation to investigate it.

## Step 4: Turning Python Findings into an Interactive Power BI Dashboard

After completing the Python EDA, I developed an interactive Power BI dashboard titled **Books Analysis**. It presented the findings through KPI cards, charts, and filters.

The dashboard highlighted four key metrics:

- **Total books:** 1,000
- **Average price:** £35.07
- **Median price:** £35.98
- **Average rating:** 2.92 out of 5

The rating distribution chart confirmed that one-star books were the largest category. The median-price comparison showed that four-star books had the highest median price at **£37.80**, while three-star books had the lowest at **£33.78**.

The price distribution histogram illustrated how books were spread across different price ranges. Meanwhile, the catalogue-page chart showed fluctuations in average prices, with some pages averaging close to £30 and others exceeding £40.

These differences are worth investigating, although the chart alone cannot explain why prices varied between pages.

### Exploring the Dashboard Interactively

I included three slicers to help users explore the dataset:

- **Rating:** Filter books by star rating.
- **Availability:** Filter books by stock status.
- **Page:** Focus on individual catalogue pages.

These filters made it easier to compare different groups of books without manually modifying the dataset. However, the availability filter had limited analytical value because all 1,000 collected books were marked as in stock.

## Key Observations

The combined Python and Power BI analysis produced six important findings:

- The scraping process successfully collected 1,000 book records across 50 pages.
- The average and median prices were approximately £35.
- One-star books formed the largest rating category, accounting for 22.6% of the dataset.
- Four-star books had the highest average and median prices, but five-star books were not the most expensive on average.
- Price and rating had almost no linear relationship in the collected data.
- Average prices varied across catalogue pages, while the absence of different stock statuses limited availability analysis.

## Recommendations and Next Steps

Based on these findings, I identified several opportunities to improve the project.

### Expand the Dataset

Additional attributes, such as book category, publisher, and publication date, could help explain differences in price and ratings.

### Strengthen Data Validation

Checking for missing values, duplicate records, invalid prices, and unexpected ratings would improve confidence in the results.

### Investigate Price Outliers

Using quartiles and the interquartile range could help identify unusually expensive or inexpensive books.

### Improve the Dashboard

Adding minimum and maximum price KPIs, a reference line for the overall average, and clearer chart labels would make comparisons easier.

### Collect More Availability Data

Capturing stock information at different times could help reveal changes in availability and support more meaningful comparisons.

### Maintain Consistency Across Tools

The calculations in Power BI should match those in Python to ensure that both stages of the project communicate the same findings.

## Conclusion

This project took me from raw website data to meaningful insights using Python and Power BI. By scraping and analyzing 1,000 book records, I discovered that higher prices do not necessarily mean higher ratings. The interactive dashboard brought these findings to life, turning raw data into clear, actionable insights.

**My biggest takeaway? Data analytics is not just about collecting data; it is about transforming it into insights that tell a story.**

## Tools and Technologies

- Python
- Requests
- BeautifulSoup
- Pandas
- NumPy
- Matplotlib
- Power BI
- CSV and Excel
