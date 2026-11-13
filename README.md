# powerbi-customer-analysis
A good first portfolio project is a retail sales and customer analysis report. It teaches the full workflow employers expect: importing data, cleaning it, modeling it, writing DAX measures, designing useful report pages, and explaining what the numbers mean.

# Project brief
Imagine a retailer asks:
“Which products, customers, and markets are driving sales? Where are returns or weak results hurting us?”

You’ll answer that with an interactive report built from the [public UCI Online Retail dataset](https://archive.ics.uci.edu/dataset/352/online+retail). It contains online retail transactions from a UK based business covering December 2010 to December 2011. It’s a useful practice dataset, though it is historical, so don’t present its figures as current market facts.

# Build it in this order
1. Get Power BI Desktop and inspect a sample report.
   Start with Microsoft’s Power BI Desktop getting started tutorial. You can also open a Microsoft sample .pbix to see how an existing report is structured. Treat the sample as something to learn from, then build your own.
2. Import the retail data and clean it in Power Query.
   Use Get data to import the dataset, then Transform data to open Power Query. Check column names and data types, inspect blank customer IDs, and investigate cancelled invoices or negative quantities before deciding how to handle them. Keep the raw source intact and make repeatable transformations in Power Query.
3. Create a model that makes questions easy to answer.
   The source may arrive as one large transaction table. Aim to organize the model around a sales fact table and dimensions such as Date, Product, and Customer. A fact table stores events and values to summarize; dimensions provide the fields people use to filter and group results. This is the star schema pattern recommended in Microsoft’s Power BI modeling guidance.
4. Write explicit DAX measures.
   Start with measures such as:
   `
        Revenue =
            SUMX(
                Sales,
                Sales[Quantity] * Sales[UnitPrice]
            )

        Units Sold =
            SUM(Sales[Quantity])

        Orders =
            DISTINCTCOUNT(Sales[InvoiceNo])

        Average Order Value =
            DIVIDE([Revenue], [Orders])
    
   