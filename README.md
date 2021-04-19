# Sample OData Application

## Artifacts

* **Orders.schema** - the database layout
* **Orders.odata** - the OData descriptor
* **ORDERS.append** and **ITEMS.append** - the sample data
* **OrdersHandler.js** - the callback function
* **CreateOrderRequest.txt** - a sample create request

## Deploy

1. Download the sample as [ZIP file](https://github.com/dirigiblelabs/sample-odata/archive/refs/heads/master.zip)
2. Upload via [Import View](https://www.dirigible.io/help/development/ide/views/import/)
3. Publish the project from the popup [menu](https://www.dirigible.io/help/development/concepts/publishing/)
4. Open URL: ```http://localhost:8080/odata/v2/```
5. You should be able to see after a while the collections for Orders and Items:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<service xmlns="http://www.w3.org/2007/app" xmlns:atom="http://www.w3.org/2005/Atom" xml:base="http://localhost:8080/odata/v2/">
   <workspace>
      <atom:title>Default</atom:title>
      <collection href="Orders">
         <atom:title>Orders</atom:title>
      </collection>
      <collection href="Items">
         <atom:title>Items</atom:title>
      </collection>
   </workspace>
</service>
```

## Create Entry

1. Via POST request tool by your choice execute the request from **CreateOrderRequest.txt**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xml:base="http://localhost:8080/odata/v2/">
   <id>http://localhost:8080/odata/v2/Orders(101)</id>
   <title type="text">Orders</title>
   <updated>2021-04-19T13:33:17.097+03:00</updated>
   <category term="org.apache.olingo.odata2.ODataOrders.OrdersType" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
   <link href="Orders(101)" rel="edit" title="OrdersType" />
   <content type="application/xml">
      <m:properties>
         <d:Id>101</d:Id>
         <d:Customer>John</d:Customer>
      </m:properties>
   </content>
</entry>
```

2. In the logs you should see the line:

> before create order event has been triggered

which comes from the callback handler **OrdersHandler.js**, which is configured in the OData descriptor **Orders.odata**
