# Chinook

## Possible solution for the below questions

1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
```
SELECT
	CustomerId ,
	FirstName ,
	LastName ,
	Country
FROM
	Customer
WHERE
	Country <> 'USA'
```
2. Provide a query only showing the Customers from Brazil.
```
SELECT
	CustomerId ,
	FirstName ,
	LastName 
FROM
	Customer
WHERE
	Country = 'Brazil'
```
3. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
```
SELECT
	FirstName,
	LastName ,
	InvoiceId ,
	InvoiceDate ,
	BillingCountry 
FROM
	Customer
INNER JOIN Invoice ON
	Customer.CustomerId = Invoice.CustomerId
WHERE
	Country = 'Brazil'
```
4. Provide a query showing only the Employees who are Sales Support Agents.
```
SELECT
	*
FROM
	Employee
WHERE 
	Title = 'Sales Support Agent'
```
5. Provide a query showing a unique list of billing countries from the Invoice table.
```
SELECT
	DISTINCT 
	BillingCountry
FROM
	Invoice
```
6. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
```
SELECT 
    Invoice.InvoiceId,
    Employee.EmployeeId,
    Employee.FirstName,
    Employee.LastName,
    Invoice.Total
FROM
    Customer
        JOIN
    Invoice ON Customer.CustomerId = Invoice.CustomerId
        JOIN
    Employee ON Customer.SupportRepId = Employee.EmployeeId
```
7. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
```
SELECT 
    Customer.FirstName,
    Customer.LastName,
    Customer.Country,
    Employee.FirstName,
    Employee.LastName,
    Invoice.InvoiceId,
    Invoice.Total
FROM
    Customer
        JOIN
    Invoice ON Customer.CustomerId = Invoice.InvoiceId
        JOIN
    Employee ON Customer.SupportRepId = Employee.EmployeeId
```
8. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
```
SELECT 
    EXTRACT(YEAR FROM InvoiceDate) AS Year,
    COUNT(InvoiceId) AS 'No. of Invoices',
    SUM(Total)
FROM
    Invoice
WHERE
    EXTRACT(YEAR FROM InvoiceDate) BETWEEN 2009 AND 2011
GROUP BY EXTRACT(YEAR FROM InvoiceDate)
```
9. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
```
SELECT 
	InvoiceId,
    SUM(Quantity)
FROM
    InvoiceLine
WHERE
    InvoiceId = 37
```
10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY
```
SELECT 
	InvoiceId,
    SUM(Quantity)
FROM
    InvoiceLine
GROUP BY
	InvoiceId
```
11. Provide a query that includes the track name with each invoice line item.
```
SELECT 
    InvoiceLine.InvoiceLineId, Track.Name
FROM
    InvoiceLine
        JOIN
    Track ON InvoiceLine.TrackId = Track.TrackId
ORDER BY InvoiceLine.InvoiceLineId
```
12. Provide a query that includes the purchased track name AND artist name with each invoice line item.
```
SELECT 
    InvoiceLine.InvoiceLineId, Track.Name, Artist.Name
FROM
    InvoiceLine
        JOIN
    Track ON InvoiceLine.TrackId = Track.TrackId
        JOIN
    Album ON Track.AlbumId = Album.AlbumId
        JOIN
    Artist ON Album.ArtistId = Artist.ArtistId
ORDER BY InvoiceLine.InvoiceLineId
```
13. Provide a query that shows the # of invoices per country. HINT: GROUP BY
```
SELECT 
    BillingCountry AS Country, COUNT(InvoiceId)
FROM
    Invoice
GROUP BY BillingCountry
```
14. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be included on the resultant table.

15. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.

16. Provide a query that shows all Invoices but includes the # of invoice line items.

17. Provide a query that shows total sales made by each sales agent.

18. Which sales agent made the most in sales in 2009? Steve Johnson - $164.34

19. Which sales agent made the most in sales in 2010? Jane Peacock - 221.92

20. Which sales agent made the most in sales over all? Jane Peacock -	833.04

21. Provide a query that shows the # of customers assigned to each sales agent.

22. Provide a query that shows the total sales per country. Which country's customers spent the most? USA

23. Provide a query that shows the most purchased track of 2013.

24. Provide a query that shows the top 5 most purchased tracks over all.

25. Provide a query that shows the top 3 best selling artists.

26. Provide a query that shows the most purchased Media Type.

27. Provide a query that shows the number tracks purchased in all invoices that contain more than one genre.
