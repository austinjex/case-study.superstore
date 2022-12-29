  <h2>Case Study #1: Superstore Sales Data</h2>
    </div>
    <p style = text-align:center>
      First published: December 28, 2022
      <br>
      Last modified: December 28, 2022</p> 
    
  <h3>Background</h3>
  <p style = "font-size:140%;">Superstore Sales is a public dataset containing 10,000 rows of product sales information from a ficticious company called Superstore. The store sells mostly office supplies. The sales data spans a 4 year period. It features 3,312 different items, sold in 604 cities across the contiguous United States.
  
  The last year of record in the datset is 2017, which will be referred to as "last year" only for the purposes of this case study. 
  I will refer to 2017 as "last year" for the sake of my case study because this data analysis would only be useful to begin with if Superstore is still in business and has a future. 
  This assumption is justified because the datset is fictitious to begin with and is an otherwise useful datset to practice on.
  Another assumption I'm making is that each unique city in the dataset has only 1 store in it. The dataset makes no mention of store locations, so this assumption is necessary. If this datset were not fictitious, or if that information were discoverable, I would not proceed with analysis without knowing for certain whether each unique city only has 1 store or if there are multiple stores in some cities. 
  But seeing as I cannot know these facts and Superstore is a ficticious company, I will just work based on the assumption that each unique city has only 1 Superstore.
  </p> 

  <h3>Case Study Process</h3>
  <p style = "font-size:140%;">For this case study, I was tasked with coming up with my own business questions for a dataset of my choice. I followed the data analytics process of <b>ask, prepare, process, analyze, share, and act</b> for my case study. 
    My case study is divided into subheadings based on these 6 phases of the data analytics process.
  </p> 
  
<!--Ask-->
  <h3>Ask</h3>
  <p style = "font-size:140%;">In this phase, I asked questions about the dataset that would help me determine the business problem and how I would go about solving the business problem through my analysis. I also defined my audience during this phase so that I could prepare my analysis with the goal in mind of sharing the findings with the right people. 
  During the ask phase, I determined that <b>the primary business problem is that Superstore needs to be making more profit.</b> I quickly noticed while skimming the dataset that certain transactions have a negative profit, while others have close to no profit. 
 <br><br> I determined that <b>the purpose of my data analysis is to find which products and store locations are the least profitable and which products and store locations are the most profitable.</b> I believe that with this information, Superstore can make data-driven decision about which products to restock, which products to discontinue, and which stores may need additional training and/or resources to become profitable.
</p>
<!--Prepare-->
<h3>Prepare</h3>
<p style = "font-size:140%;">This phase of data analysis included documenting where the data came from, determining the data format, and storing data properly.
The "Superstore Sales" dataset was downloaded from Tableau Public's "Resources" page under "Sample Data." <a href="https://public.tableau.com/app/resources/sample-data">Here's a link to the Tableau Public Sample Data webpage.</a>
<br><br>
The dataset has 21 columns: Row ID, Order ID, Order Date, Ship Date, Ship Mode, Customer ID, Customer Name, Segment, Country, City, State, Postal Code, Region, Product ID, Category, Sub-Category, Product Name, Sales, Quantity, Discount, and Profit.
All of these columns were originally formatted as string data type, excpet for Order Date and Ship Date, which were formatted as dates (MM/DD/YYYY).
<br><br>
Some common data format dimensions are internal vs. external, qualitative vs. quantitative, nominal vs. ordinal, continuous vs. discrete, and structured vs unstructered.
This dataset could be described as being external data because I was able to download it as a publicly available dataset as opposed to having to access it from a private database. 
The qualitative data includes data from the following columns: Ship Mode, Customer Name, Segment, Country, City, State, Region, Category, Sub-Category, and Product Name. The other 11 columns contain quantitative data. 
All 10 of the qualitative data columns contain nominal data (none of them are ordinal). 
Of the 11 quantitative data columns, the following contain continuous data: Sales, Quantity, Discount, and Profit. The other 7 quantitative columns contain discrete data. 
All 21 columns contain structured data (none of them are unstructured).
<br><br>
As for the storage of this dataset, after downloading the file from Tableau Public, I saved it as "CaseStudy.Superstore.Dec2022.v1" as a CSV UTF-8 (Comma delimited) (*.csv) file. This format is simple and neat, and it helps me understand what is in the file. This file type will make it easy for me to upload the file for analysis using SQL later on in the process. I stored the file in a folder on my desktop called "Case Studies."
<!--Prepare End-->
<!--Process-->

<h3>Process</h3>
<p style = "font-size:140%;">This phase of the data analyis process involved cleaning the data. To ensure the data was clean, I checked each column for missing values using filtering in Excel, checked for misspelled words by using filtering in Excel, checked for numeric values that didn't make sense using filtering in Excel, and made sure that products with the same product ID had the same categorizations using filtering in Excel. I was surprised to find out that the data was already very clean. There were no missing values in any of the over 200,000 cells. There were no misspelled words. The numbers seemd to add up perfectly. The cleanliness of the data made it evident to me that the dataset must have been cleaned by whoever published the public dataset originally.  
  The only issue I found was related to the postal codes. 
  <br><br>
  Certain postal codes in the United States begin with a 0 as the first digit. Because the Postal Codes column was formatted with "General" as the data type, these postal codes that started with a 0 ended up being interpretted as whole integars by Excel, and were displayed as 4-digit numbers, omitting the 0 at the start. I filtered the spreadsheet so that only these 4-digit postal codes were visible, and I saw that there were 449 rows of orders in these postal codes. To make it so that all 5 digits were visible, I highlighted the whole column and changed the data type from "General" to "ZIP Code". All of the 4-digit postal codes changed to include a 0 as the first digit. 
  I went through and checked 25 or so of the newly formatted rows to make sure that the postal code was appropriate based on the corresponding city and state. They were all correct, so I trusted that Excel had properly converted the values in the Postal Code column to the correct ZIP codes. 
  With that complete, I concluded that the data was all clean.
</p> 
<!--Process End-->
<!--Analyze-->

<h3>Analyze</h3>
<p style = "font-size:140%;"> This phase of the data analysis process involved <b>organizing data and identifying trends and relationships within the data to solve business problems.</b> One of the ways I organized data to find patterns was by filtering and sorting the data in Excel. I used sorting in Excel to get an idea of the range of values for certain columns. One example of this was sorting the data by Profit in descending order so that I could see the sales which resulted in the highest profits and lowest profits. An example of a filter I chose was filtering out all of the sales data except for a select city. By doing this, I could see what one store might sell over a period of time. Speaking of period of time, the filter I used most often during my analysis phase was a filter by order date. I was especially interested in recent data because it would be a better reflection of the current performance of the company than older data. For that reason, I chose to filter data during most of my analysis to only include the data from the most recent year. Thus, filtering and sorting in Excel helped me organize data in a way that made it easier to identify trends and relationships. 
<br><br>
In additon to Excel, I also used SQL to organize and analyze the dataset. I uploaded the dataset to BigQuery, a Google Cloud service, so that I could query the dataset and find trends I was interested in analyzing. 
While making these queries, I kept in mind that the purpose of my data analysis is to find which products and store locations are the least profitable and which products and store locations are the most profitable.
The following are some of my queries that I found insightful, starting with a query of all 410 <b>cities ordered by total profit last year (highest to lowest)</b>.
</p>
<br><br>
<!--QUERIES-->
<pre style = "font-size:140%;">
      SELECT 
              CONCAT(City, ",", " ", State),
              ROUND(SUM(Profit),2) AS total_profit_USD, 
              COUNT(Row_ID) AS number_of_orders, 
              ROUND(SUM(Sales),2) AS total_sales_USD,  
              SUM(Quantity) AS total_quantity_of_products_sold,
              ROUND((SUM(Sales)/COUNT(Row_ID)),2) AS average_sale_per_order_USD,
              ROUND((SUM(Profit)/COUNT(Row_ID)),2) AS average_profit_per_order_USD,
              (ROUND(AVG(Discount),1)) * 100 AS average_discount_percent
      FROM 
              `superstore-371700.superstore.orders`
      WHERE
              LEFT(CAST(Order_Date AS string), 4) = '2017'
      GROUP BY
              CONCAT(City, ",", " ", State)
      ORDER BY
              total_profit_USD DESC

-- This query displays certain metrics for each city in our dataset. 
It lists the cities in order of total profit, with highest total profit first and lowest total profit last.
It is also filtered to only show data from 2017. Remember that I'm making the assumption for the sake of this case study on ficticious data that last year was 2017. --
</pre>
<br><br>
<p style = "font-size:140%;">Below are the first 10 rows of the results table that was generated when I ran this query (showing <b>cities ranked by total profit last year from highest to lowest</b>):</p>
<br><br>


<!--Images-->

![queryscreenshot 1](https://user-images.githubusercontent.com/109719293/209891322-111f2f20-4eda-474a-b500-43a25afd4111.jpg)
<br><br>
<p style = "font-size:140%;">By simply removing the "DESC" from the ORDER BY clause, we can find the <b>cities ranked by total profit last year from lowest to highest</b>. Here are the first 10 results of that query:</p>
<br><br>

![queryscreenshot 2](https://user-images.githubusercontent.com/109719293/209891397-6aaf8899-b36c-428e-9d1a-2c035b70c47b.jpg)

<br><br>
<p style = "font-size:140%;">The results of this query reveal something important about our dataset: <b>lots of stores are losing money!</b> In fact, when I scroll down the list of results on BigQuery, <b>the first 88 cities all have total profits below $0.00</b> for last year.
Evidently, Superstore has some serious business problems that need solving. Recognizing these unprofitable stores is a good start to solving their business problems.
<br><br>
Another important query is a ranking of each store by average profit. While total profit is certainly important, average profit will allow us to see which store are profitting the most (and the least) per sale. This is important to know because sales volume differs so much from one city to another(due to factors such as the city's population or local competetitors). Seeing the average profit per sale will help Superstore understand better which stores are performing well (and not so well) regardless of sales volume.
Below are some queries ranking <b>cities by average profit per sale:</b> </p>
<br><br>
<pre style = "font-size:140%;">
      SELECT 
              CONCAT(City, ",", " ", State),
              ROUND((SUM(Profit)/COUNT(Row_ID)),2) AS average_profit_per_order_USD,
              ROUND(SUM(Profit),2) AS total_profit_USD, 
              COUNT(Row_ID) AS number_of_orders, 
              ROUND(SUM(Sales),2) AS total_sales_USD,  
              SUM(Quantity) AS total_quantity_of_products_sold,
              ROUND((SUM(Sales)/COUNT(Row_ID)),2) AS average_sale_per_order_USD,
              (ROUND(AVG(Discount),1)) * 100 AS average_discount_percent
      FROM 
              `superstore-371700.superstore.orders`
      WHERE
              LEFT(CAST(Order_Date AS string), 4) = '2017'
      GROUP BY
              CONCAT(City, ",", " ", State)
      ORDER BY
              average_profit_per_order_USD DESC

-- This query displays certain metrics for each city in our dataset. It is filtered to only show data from 2017 ("last year"). 
It lists the cities in order of average profit per order, with highest average profit first and lowest average profit last. --
</pre>
<br><br>
<p style = "font-size:140%;">Below are the first 10 rows of the results table that was generated when I ran this query <b>(cities ranked by average profit per order, highest to lowest):</b></p>
<br><br>

![queryscreenshot 3](https://user-images.githubusercontent.com/109719293/209891420-0c8eabaa-7601-4be5-86fd-e1cbb073b2cd.jpg)

<br><br>
<p style = "font-size:140%;">And again, by removing the "DESC" (descending) qualifier from the ORDER BY clause, we get the <b>cities ordered by average profit per sale from lowest to highest:</b></p>
<br><br>

![queryscreenshot 4](https://user-images.githubusercontent.com/109719293/209891588-1ef23586-706f-4d21-8205-285ccafd8cd1.jpg)

<br><br>
<p style = "font-size:140%;">These queries contain useful insights for Superstore. These queries show which cities are performing well and which cities are struggling. Superstore can use the results of these queries to inform their business decisions. As a dta analyst, I can show the stakeholders at Superstore these results and allow them to use their subject matter expertise to interpret the results. Perhaps the stakeholders will decide that certain stores with negative profit should be shut down and liquidated. Perhaps they know that certain stores are brand new and just need time to grow. Perhaps they know which stores have fierce competitors nearby and others that have notoriously poor managers. Whatever the case may be, <b>the stakeholders can use the results of these queries combined with the subject matter expertise to make data-driven decsions.</b> But first, there are other insights to find.
<br><br>
After seeing the results of the previous queries, I noticed a pattern, which is that <b>the cities with the lowest profit tended to have the highest average discounts.</b>This insight alone is somewhat valuable, but it is not a solution in and of itself. The higher average discounts could be caused by those stores offering too many discounts, having worse products on their shelves that require higher discounts in order to get sales, or there could be some super-shoppers at those locations who are extremely talented at using coupons. Or it could be yet another unseen factor. Because our data does not make mention of promotional discount offers or coupons, I cannot investigate those potential causes any further. I can, however, make the stakeholders aware of this pattern. I intend to do so later in the data analysis process.
<br><br>
As for the quality of products on the shelves, I can offer further insight using other queries. 
Below are some insightful queries related to the quality of the products sold last year, starting with <b>products ranked by total profit last year from highest to lowest:</b> </p>
<br><br>
<pre style = "font-size:140%;">
      SELECT 
              Product_ID, 
              Product_Name,
              Category,
              Sub_Category,
              ROUND((Profit * Quantity),2) AS total_profit,
              ROUND(Profit,2) AS average_profit,
              Quantity AS quantity_sold
      FROM 
              `superstore-371700.superstore.orders`
      WHERE
              LEFT(CAST(Order_Date AS string), 4) = '2017'
      ORDER BY 
              total_profit DESC

-- This query shows the products that had the best total profits in 2017 ("last year"). It is sorted from highest to lowest total profit. --
</pre>
<br><br>
<p style = "font-size:140%;">Below are the first 10 rows of the results from this query <b>(products ranked by total profit highest to lowest):</b></p>
<br><br>

![queryscreenshot 5](https://user-images.githubusercontent.com/109719293/209891632-9ce93b37-d9a7-4bde-bac7-ae0aa568a184.jpg)

<br><br>
<p style = "font-size:140%;">And the same query <b>ordered by total profit in ascending order (lowest to highest)</b> gives the following results (showing only the first 10 results):</p>
<br><br>

![queryscreenshot 6](https://user-images.githubusercontent.com/109719293/209891693-a4134eca-d18e-47f7-b96f-637e8603ca83.jpg)

<br><br>
<p style = "font-size:140%;">In addition to ranking products by total profit, I found it useful to rank products by average profit as well. Here are the first 10 results from a query of <b>products ranked by average profit per order, highest to lowest.</b></p>
<br><br>

![queryscreenshot 7](https://user-images.githubusercontent.com/109719293/209891714-72f477d7-6c61-479e-bde3-aff8bb54366a.jpg)

<br><br>
<p style = "font-size:140%;">And the same query <b>ordered by average profit, lowest to highest </b>(by removing the "DESC" from the ORDER BY clause) gives the following results (showing only the first 10 results):</p>
<br><br>

![queryscreenshot 8](https://user-images.githubusercontent.com/109719293/209891741-f186b898-6dd8-42c7-9eae-ea6f52f81721.jpg)

<br><br>
<p style = "font-size:140%;">These queries provide insights about which products profitted the most for Superstore last year, and which products lost Superstore money last year. 
These queries, along with the queries about the profit of each city, fulfill the purpose of our data analysis, which was to find which products and store locations are the least profitable and which products and store locations are the most profitable.
<b>Using the insights from these queries and their own subject matter expertise, Superstore's stakeholders can make data-driven decisions to solve their business problem, increasing the profit of Superstore.</b>
To make these insights easier and quicker to understand, I also used Tableau to visualize the data during the Share phase of my process.
</p>
<!--Analyze End-->
<!--Share-->

<h3>Share</h3>
<p style = "font-size:140%;">The Share phase of the data analytics process is one of the most important phases. Without sharing the insights of my analysis, none of the work I've done so far will help Superstore solve business problems. 
During this phase of my case study, I made the insights from my analysis easy for stakeholders to understand. Specifically, I used Tableau to visualize the data so that the insights of my analysis would be easy to access and understand.
I uploaded the dataset to Tableau Public and created a few dashboards that I thought would display the findings of my analysis clearly.
<br><br>
I mentioned during the Ask phase that one thing I determined at that time was who my audience was. It is important to mention that my dataset had a tab titled "People" which showed a person for each region of Superstore. I assume that these people must be Superstore regional mangers of some sort. 
Thus, my audience for the Share phase includes the Superstore stakeholders (company executives, investors, managers, department leaders, etc) and the four regional managers. Because the regional managers are part of my audience, the data visualization dashboards include visualizations specific to each region. <b>With dashboards for overall company data and region-specific data, all members of the audience have useful data insights, visualized in a way that is simple and easy to understand.</b>
<br><br>
Below are my embedded interactive data visualization dashboards. Notice that there are 8 tabs, each with a unique dashboard, hovering the cursor over graphical elements reveals data labels, the maps have panning and zooming capabilities, and the graphs with many line items have a scroll bar. 
Zooming in or out on the webpage may make the visualizations easier to view and interact with. If the visualizations are not viewable on your device, try viewing them on Tableau Public using the link below:
<br><br>
<a href="https://public.tableau.com/views/SuperstoreSalesDataVisualization_16711277420240/Locations_1?:language=en-US&:display_count=n&:origin=viz_share_link">View Superstore Sales Data Vizualization by Austin Jex</a>

<br><br>
<div class='tableauPlaceholder' id='viz1672189445379' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Su&#47;SuperstoreSalesDataVisualization_16711277420240&#47;Locations_1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='SuperstoreSalesDataVisualization_16711277420240&#47;Locations_1' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Su&#47;SuperstoreSalesDataVisualization_16711277420240&#47;Locations_1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div>                
</p> 
<!--Share End-->
<!--Act-->

<h3>Act</h3>
<p style = "font-size:140%;">The Act phase is the time for applying insights and making decisions that solve problems. During this phase, I made recommendations to the audience regarding actions Superstore should take to solve the business problem, which is raising Superstores profits. 
Based on the insights from my data analysis, it is my recommendation that Superstore take the following actions to increase their profits:
<br><br>
1. Discontinue products sold last year whose average profit was less than $0.10 per item. This list includes 639 of the 3,312 products sold last year. The profit from these items alone last year was -$53,836.19. Superstore should also use the disconinuation of these low-profit products as an opportunity to stock higher quantities of high-profitting products in their place.
<br><br>
2. Show off top profitting products at multiple places in stores. As an example, there were 550 products last year with average profits per item above $50.00. The smaller of these items could be displayed on aisle endcaps and shelves near the checkout in addition to their respective locations in-store.
<br><br>
3. Keep discounts to a minimum (average discount per transaction should be 10% at most). Do not offer any discounts above 20%.
<br><br>
4. Hold additional meetings regarding the stores that had total profits less than $0.00 (this includes 88 of the 410 stores). Subject matter expertise is needed for decision-making, but some action should be taken to improve performance or discontinue operations at these stores.
<br><br>
5. Further analysis should be done on the best and worst performing stores to find factors that predict high and low profitting stores.</li>
<br><br>
As stated above, further analysis should be conducted to identify factors that predict a store's success. This analysis would ideally include data other than just the sales data included in the present dataset. Examples of useful data to collect for this analysis might include customer feedback, employee count, employee tenure, manager tenure, quality of stocked products, size of store, and other factors deemed important by the subject matter experts.
<br><br>
Although further analysis would certainly be helpful, I am confident that the application of the above recommendations by Superstores stakeholders will result in increased profits for Superstore.
</p>
