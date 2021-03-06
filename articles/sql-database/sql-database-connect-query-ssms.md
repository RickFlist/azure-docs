---
title: 'SSMS: Connect and query data in Azure SQL Database | Microsoft Docs'
description: Learn how to connect to SQL Database on Azure by using SQL Server Management Studio (SSMS). Then, run Transact-SQL (T-SQL) statements to query and edit data.
metacanonical: ''
keywords: connect to sql database,sql server management studio
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''

ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: development
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: carlrab

---
# Azure SQL Database: Use SQL Server Management Studio to connect and query data

[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is used to create and manage SQL Server resources from the user interface or in scripts. This guide details using SSMS to connect to an Azure SQL database, and then execute query, insert. update, and delets statements.

This quick start uses as its starting point the resources created in one of these quick starts:

- [Create DB - Portal](sql-database-get-started.md)
- [Create DB - CLI](sql-database-get-started-cli.md)
- [Create DB - Powershell](sql-database-get-started-powershell.md) 

Before you start, make sure you have installed the newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx). 

## Get connection information

Get the fully qualified server name for your Azure SQL Database server in the Azure portal. You use this name to connect to your server using SQL Server Management Studio.

1. Log in to the [Azure portal](https://portal.azure.com/).
2. Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page. 
3. In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.

    ![connection information](./media/sql-database-connect-query-ssms/connection-information.png)

## Connect to the server

Use SQL Server Management Studio to establish a connection to your Azure SQL Database server with SQL Server authentication.

1. Type **SSMS** in the Windows search box and then click **Enter** to open SSMS.

2. In the **Connect to Server** dialog box, enter the following information:
   - **Server type**: Database engine
   - **Server name**: the fully qualified server name in the form of **mynewserver20170313.database.windows.net**
   - **Authentication**: SQL Server Authentication
   - **Login**: your server admin account
   - **Password**: the password for your server admin account
 
    ![connect to server](./media/sql-database-connect-query-ssms/connect.png)
3. Click **Connect**. The Object Explorer window opens in SSMS. 

    ![connected to server](./media/sql-database-connect-query-ssms/connected.png)
4. In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.

## Query data

Use the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement to query data in your Azure SQL database.

1. In Object Explorer, right-click **mySampleDatabase** and click **New Query**. A blank query window opens that is connected to your database.
2. In the query window, type the following query in the query window to retrieve data from the Product and ProductCategory tables:

   ```tsql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. On the toolbar, click **Execute**.

    ![query](./media/sql-database-connect-query-ssms/query.png)

## Insert data

Use the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transcat-SQL statement to insert data into your Azure SQL database.

1. On the toolbar, click **New Query**. A blank query window opens connected to your database.
2. In the query window, type the following query in the query window to insert a new row in the Product table:

   ```tsql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
		   , [StandardCost]
		   , [ListPrice]
		   , [SellStartDate]
		   )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
		   ,100
		   ,100
		   ,GETDATE() );
   ```

3. On the toolbar, click **Execute**.

    ![insert](./media/sql-database-connect-query-ssms/insert.png)

4. In the query window, use the following query to view the newly added product:

   ```tsql
   SELECT [ProductId]
	, [Name]
	, [ProductNumber]
	, [Color]
	, [StandardCost]
	, [ListPrice]
	, [SellStartDate] 
   FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

    ![insert](./media/sql-database-connect-query-ssms/inserted-query.png)


## Update data

Use the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement to update data in your Azure SQL database.

1. On the toolbar, click **New Query**. A blank query window opens connected to your database.
2. In the query window, type the following query in the query window to update a row in the Product table:

   ```tsql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

3. On the toolbar, click **Execute**.

    ![update](./media/sql-database-connect-query-ssms/update.png)

4. In the query window, use the following query to view the updated list price for the product:

   ```tsql
   SELECT [ProductId]
	, [Name]
	, [ListPrice]
   FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

    ![updated query](./media/sql-database-connect-query-ssms/updated-query.png)

## Delete data

Use the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement to delete data in your Azure SQL database.

1. On the toolbar, click **New Query**. A blank query window opens connected to your database.
2. In the query window, type the following query in the query window to delete a row in the Product table:

   ```tsql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

3. On the toolbar, click **Execute**.

    ![delete](./media/sql-database-connect-query-ssms/delete.png)

4. In the query window, use the following query to verify the row was deleted:

   ```tsql
   SELECT [ProductId]
	, [Name]
	, [ProductNumber]
	, [Color]
	, [StandardCost]
	, [ListPrice]
	, [SellStartDate] 
   FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

    ![deleted query](./media/sql-database-connect-query-ssms/deleted-query.png)

## Next steps

- For more information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
- For a getting started with SQL Server authentication tutorial, see [SQL authentication and authorization](sql-database-control-access-sql-authentication-get-started.md).
- For a getting started with Azure Active Directory authentication tutorial, see [Azure AD authentication and authorization](sql-database-control-access-aad-authentication-get-started.md).
