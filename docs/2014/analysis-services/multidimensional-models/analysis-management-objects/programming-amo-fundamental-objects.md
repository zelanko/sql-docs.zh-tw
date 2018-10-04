---
title: 程式設計 AMO 基礎物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- server objects [AMO]
- programming [AMO]
- AMO, database objects
- AMO, server objects
- Analysis Management Objects, server objects
- database objects [AMO]
- Analysis Management Objects, database objects
ms.assetid: 3f1ab656-f3bc-432d-8b6d-cdf204e5be10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc100d99d3e125c22c04aac8cf092646f2b0cfa1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168988"
---
# <a name="programming-amo-fundamental-objects"></a>程式設計 AMO 基礎物件
  基礎物件通常是簡單且直接的物件。 通常會建立和具現化這些物件，然後當不再需要時，使用者會將它們中斷連接。 基礎類別包括下列物件：<xref:Microsoft.AnalysisServices.Server>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataSource> 和 <xref:Microsoft.AnalysisServices.DataSourceView>。 在 AMO 基礎物件中唯一屬於複雜物件的是 <xref:Microsoft.AnalysisServices.DataSourceView>，這需要詳細資料以建立代表資料來源檢視的抽象模型。  
  
 通常需要 <xref:Microsoft.AnalysisServices.Server> 與 <xref:Microsoft.AnalysisServices.Database> 物件以使用所含物件做為 OLAP 物件或是資料採礦物件。  
  
 本主題包含下列幾節：  
  
-   [伺服器物件](#ServerObjects)  
  
-   [AMOException 例外狀況物件](#AMO)  
  
-   [資料庫物件](#DatabaseObjects)  
  
-   [DataSource 物件](#DataSource)  
  
-   [DataSourceView 物件](#DSV)  
  
##  <a name="ServerObjects"></a> 伺服器物件  
 使用 <xref:Microsoft.AnalysisServices.Server> 物件需要下列步驟：連接到伺服器、確認 <xref:Microsoft.AnalysisServices.Server> 物件是否連接到伺服器，如果已連接，則從伺服器中斷連接 <xref:Microsoft.AnalysisServices.Server>。  
  
### <a name="connecting-to-the-server-object"></a>連接到伺服器物件  
 連接到伺服器必須有正確的連接字串。  
  
 下列程式碼範例會在連接成功時傳回 <xref:Microsoft.AnalysisServices.Server> 物件，或是在錯誤發生時傳回 `null`。 在連接處理期間所發生的錯誤，會在 Try/Catch 建構中處理。 AMO 錯誤會透過使用 <xref:Microsoft.AnalysisServices.AmoException> 例外況狀類別來擷取。 在這個範例中，會在訊息方塊中對使用者顯示錯誤。  
  
```  
static Server ServerConnect( String strStringConnection)  
{  
    string methodCaption = "ServerConnect method";  
    Server svr = new Server();  
    try  
    {  
        svr.Connect(strStringConnection);  
    }  
    #region ErrorHandling  
    catch (AmoException e)  
    {  
        MessageBox.Show( "AMO exception " + e.ToString());  
        svr = null;  
    }  
    catch (Exception e)  
    {  
        MessageBox.Show("General exception " + e.ToString());  
        svr = null;  
    }  
    #endregion  
  
    return svr;  
}  
```  
  
 連接字串的結構是：  
  
 「**資料來源 =**\<伺服器名稱 >"。  
  
 如需有關連接字串的詳細資訊，請參閱＜<xref:Microsoft.SqlServer.Management.Common.OlapConnectionInfo.ConnectionString%2A>＞。  
  
### <a name="validating-the-connection"></a>驗證連接  
 在進行 <xref:Microsoft.AnalysisServices.Server> 物件的程式設計之前，您應該先確認是否仍然連接到伺服器。 下列程式碼範例示範如何執行這項工作。 此範例假設 `svr` 是存在於您的程式碼中的 <xref:Microsoft.AnalysisServices.Server> 物件。  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    // Do what it is needed if connection is good  
}  
```  
  
### <a name="disconnecting-from-the-server"></a>從伺服器中斷連接  
 只要您一完成，就可以透過使用 Disconnect 方法從伺服器中斷連接。 下列程式碼範例示範如何執行這項工作。 此範例假設 `svr` 是存在於您的程式碼中的 <xref:Microsoft.AnalysisServices.Server> 物件。  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    svr.Disconnect()  
}  
```  
  
###  <a name="AMO"></a> AmoException 例外狀況物件  
 AMO 在找到不同的問題時將會擲回例外狀況。 如需例外狀況的詳細說明，請參閱 < [AMO 其他類別和方法](amo-other-classes-and-methods.md)。 下列範例程式碼顯示在 AMO 中擷取例外狀況的正確方法：  
  
```  
try  
{  
   //... some AMO code in here  
}  
  
catch (  OutOfSynchException e)  
{  
   // error handling code for OutOfSynchException   
}  
  
catch (  OperationException e)  
{  
   // error handling code for OperationException   
}   
  
catch (  ResponseFormatException e)  
  
{  
   // error handling code for ResponseFormatException   
}   
  
catch (  ConnectionException e)  
  
{  
   // error handling code for ConnectionException   
}  
  
catch (  AMOException e)  
  
{  
   //... here is the place where you end if it is an AMO exception, but none of the previous exceptions  
   // if you start with AMOException in the first catch you will never see any one of the previous exceptions  
}  
```  
  
##  <a name="DatabaseObjects"></a> 資料庫物件  
 使用 <xref:Microsoft.AnalysisServices.Database> 物件非常簡單且直接。 您可以從 <xref:Microsoft.AnalysisServices.Server> 物件的資料庫集合取得現有的資料庫。  
  
### <a name="creating-dropping-and-finding-a-database"></a>建立、卸除和尋找資料庫  
 下列程式碼範例示範如何使用資料庫名稱建立資料庫。 在建立資料庫之前，請先查詢伺服器的 <xref:Microsoft.AnalysisServices.DatabaseCollection>，以查看資料庫是否存在。 如果資料庫存在，會在卸除資料庫之後建立它，如果資料庫不存在，則會建立它。 如果要卸除資料庫，則會先從資料庫集合取得資料庫。  
  
```  
static Database CreateDatabase(Server svr, String DatabaseName)  
{  
    Database db = null;  
    if ( (svr != null) && ( svr.Connected))  
    {  
        // Drop the database if it already exists  
        db = svr.Databases.FindByName(DatabaseName);  
        if (db != null)  
        {  
            db.Drop();  
        }  
  
        // Create the database  
        db = svr.Databases.Add(DatabaseName);  
        db.Update();  
    }  
  
    return db;  
}  
```  
  
 為了判斷某資料庫是否存在於資料庫集合中，會使用 FindByName 方法。 如果資料庫存在，該方法會傳回找到的資料庫物件，如果不存在，則會傳回 Null 物件。  
  
 只要 <xref:Microsoft.AnalysisServices.Database> 物件一加入資料庫集合，就必須使用伺服器的 Update 方法來更新伺服器。 無法更新伺服器將造成在伺服器中不會建立 <xref:Microsoft.AnalysisServices.Database> 物件。  
  
### <a name="processing-a-database"></a>處理資料庫  
 處理資料庫及所有的子系物件是非常簡單的，因為 <xref:Microsoft.AnalysisServices.Database> 物件包括 Process 方法。  
  
 Process 方法可包括參數，但是並非必要。 如果未指定參數，將會使用其 `ProcessDefault` 選項來處理所有的子系物件。 如需處理選項的詳細資訊，請參閱<xref:Microsoft.AnalysisServices.Database>。  
  
1.  下列範例程式碼會根據預設值處理資料庫。  
  
```  
static Database ProcessDatabase(Database db, ProcessType pt)  
{  
    db.Process( pt);  
    return db;  
}  
```  
  
##  <a name="DataSource"></a>DataSource 物件  
 <xref:Microsoft.AnalysisServices.DataSource> 物件是 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 與資料所在的資料庫之間的連結。 代表 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 基礎模型的結構描述是由 <xref:Microsoft.AnalysisServices.DataSourceView> 物件所定義。 可以將 <xref:Microsoft.AnalysisServices.DataSource> 物件視為連至資料所在的資料庫之連接字串。  
  
 下列範例程式碼會示範如何建立 <xref:Microsoft.AnalysisServices.DataSource> 物件。 此範例會確認伺服器是否仍然存在、<xref:Microsoft.AnalysisServices.Server> 物件是否已連接，以及資料庫是否已存在。 如果 <xref:Microsoft.AnalysisServices.DataSource> 物件存在，則會先予以卸除然後重新建立。 會建立有相同名稱與內部識別碼的 <xref:Microsoft.AnalysisServices.DataSource> 物件。 在此範例中，不會在連接字串上執行檢查以進行確認。  
  
```  
static string CreateDataSource(Database db, string strDataSourceName, string strConnectionString)  
{  
        Server svr = db.Parent;  
        DataSource ds = db.DataSources.FindByName(strDataSourceName);  
        if (ds != null)  
            ds.Drop();  
        // Create the data source  
        ds = db.DataSources.Add(strDataSourceName, strDataSourceName);  
        ds.ConnectionString = strConnectionString;  
  
        // Send the data source definition to the server.  
        ds.Update();  
  
        return ds.Name;  
}  
```  
  
##  <a name="DSV"></a> DataSourceView 物件  
 <xref:Microsoft.AnalysisServices.DataSourceView> 物件負責保存 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的結構描述模型。 對於保存結構描述的 <xref:Microsoft.AnalysisServices.DataSourceView> 物件，必須先建構結構描述。 結構描述會從 System.Data 命名空間，透過 DataSet 物件建構。  
  
 下列範例程式碼將建立部分的結構描述，此結構描述會包含在以 AdventureWorks 為基礎的 Analysis Services 範例專案中。 此範例會建立資料表、計算資料行、關聯和複合關聯的結構描述定義。 結構描述是保存的資料集。  
  
 範例程式碼會執行下列各項：  
  
1.  建立 <xref:Microsoft.AnalysisServices.DataSourceView> 物件。  
  
     先確認 <xref:Microsoft.AnalysisServices.DataSource> 物件是否存在；如果是 `true`，則先卸除 <xref:Microsoft.AnalysisServices.DataSource> 然後再予以建立。 如果 <xref:Microsoft.AnalysisServices.DataSource> 不存在，則會予以建立。  
  
2.  使用 <xref:Microsoft.AnalysisServices.DataSource> 連接字串開啟資料庫的連接。  
  
3.  建立結構描述。  
  
     這個結構描述是由下列項目所構成：  
  
    -   資料表定義，`AddTable()` 方法。  
  
    -   一組選擇性的計算資料行，`AddComputedColumn()` 方法。  
  
    -   一組選擇性的關聯，`AddRelation`。  
  
    -   一組選擇性的複合關聯，`AddCompositeRelations`。  
  
4.  更新伺服器。  
  
> [!NOTE]  
>  下列範例程式碼為提高可讀性已經過修剪，完整的程式碼包括在本主題的結尾。  
  
> [!NOTE]  
>  下列方法屬於範例程式碼的一部分：`AddTable`、`AddComputedColumn`、`AddRelation` 和 `AddCompositeRelation`。  
  
> [!NOTE]  
>  子句 `'WHERE 1=0'` 是為了避免查詢將資料列傳回至 `DataSet` 物件。  
  
```  
        static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
        {  
            // Create the data source view  
            DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
            if ( dsv != null)  
               dsv.Drop();  
            dsv = db.DataSourceViews.Add(strDataSourceName);  
            dsv.DataSourceID = strDataSourceName;  
            dsv.Schema = new DataSet();  
            dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
            // Open a connection to the data source  
            OleDbConnection connection  
                = new OleDbConnection(dsv.DataSource.ConnectionString);  
            connection.Open();  
  
            #region Create tables  
  
            // Add the DimTime table  
            AddTable(dsv, connection, "DimTime");  
            AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
  
            // Add the DimProductCategory table  
            AddTable(dsv, connection, "DimProductCategory");  
  
            // Add the DimProductSubcategory table  
            AddTable(dsv, connection, "DimProductSubcategory");  
            AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
            // Add the FactInternetSales table  
            AddTable(dsv, connection, "FactInternetSales");  
"DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
  
            // Add the FactInternetSalesReason table  
            AddTable(dsv, connection, "FactInternetSalesReason");  
            AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
            dsv.Update();  
  
            #endregion  
  
            // Send the data source view definition to the server  
            dsv.Update();  
  
            return dsv;  
        }  
  
        static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
        {  
            string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
            OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
            DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
  
            dataTable.ExtendedProperties.Add("TableType", "Table");  
            dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
            dataTable.ExtendedProperties.Add("DbTableName", tableName);  
            dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
        }  
  
        static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
        {  
            DataSet tmpDataSet = new DataSet();  
            tmpDataSet.Locale = CultureInfo.CurrentCulture;  
            OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
                + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
                + tableName + "] WHERE 1=0", connection);  
            DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
            DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
            dataTable.Constraints.Clear();  
            dataTable.Columns.Remove(dataColumn);  
  
            dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
            dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
                expression);  
            dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
            dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
            dataColumn = null;  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
            tmpDataSet = null;  
        }  
  
        static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
        {  
            DataColumn fkColumn  
                = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
            DataColumn pkColumn  
                = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
                + fkColumnName, pkColumn, fkColumn, true);  
        }  
  
        static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
        {  
            DataColumn[] fkColumns = new DataColumn[2];  
            fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
            fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
            DataColumn[] pkColumns = new DataColumn[2];  
            pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
            pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
                + "_" + columnName2, pkColumns, fkColumns, true);  
        }  
  
```  
  
 在範例程式碼中，`AddTable` 和 `AddComputedColumn` 方法使用 `DataAdapter` 物件的 `FillSchema` 方法，將 `DataTable` 加入 `DataSet`，並將結構描述設定成符合資料來源中的結構描述。 擴充屬性會加入所需的資訊以設定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的結構描述。  
  
 在範例程式碼中，`AddRelation` 和 `AddCompositeRelation` 方法會加入關聯資料行，端視現有結構描述與模型上的現有資料行而定。 資料行必須屬於定義在結構描述內的資料表，這些方法才能運作。  
  
 下列是完整的程式碼範例：  
  
```  
static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
{  
    // Create the data source view  
    DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
    if ( dsv != null)  
       dsv.Drop();  
    dsv = db.DataSourceViews.Add(strDataSourceName);  
    dsv.DataSourceID = strDataSourceName;  
    dsv.Schema = new DataSet();  
    dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
    // Open a connection to the data source  
    OleDbConnection connection  
        = new OleDbConnection(dsv.DataSource.ConnectionString);  
    connection.Open();  
  
    #region Create tables  
  
    // Add the DimTime table  
    AddTable(dsv, connection, "DimTime");  
    AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarYearDesc", "'CY' + ' ' + CalendarYear");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarSemesterDesc", "CASE WHEN CalendarSemester = 1 THEN 'H1'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) ELSE 'H2'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarQuarterDesc", "'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "MonthName", "EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalYearDesc", "'FY' + ' ' + FiscalYear");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalSemesterDesc", "CASE WHEN FiscalSemester = 1 THEN 'H1'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) ELSE 'H2'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalQuarterDesc", "'Q' + CONVERT(CHAR (1), FiscalQuarter) +' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalMonthNumberOfYear", "CASE WHEN MonthNumberOfYear = '1'  THEN CONVERT(int,'7') WHEN MonthNumberOfYear = '2'  THEN CONVERT(int,'8') WHEN MonthNumberOfYear = '3'  THEN CONVERT(int,'9') WHEN MonthNumberOfYear = '4'  THEN CONVERT(int,'10') WHEN MonthNumberOfYear = '5'  THEN CONVERT(int,'11') WHEN MonthNumberOfYear = '6'  THEN CONVERT(int,'12') WHEN MonthNumberOfYear = '7'  THEN CONVERT(int,'1') WHEN MonthNumberOfYear = '8'  THEN CONVERT(int,'2') WHEN MonthNumberOfYear = '9'  THEN CONVERT(int,'3') WHEN MonthNumberOfYear = '10' THEN CONVERT(int,'4') WHEN MonthNumberOfYear = '11' THEN CONVERT(int,'5') WHEN MonthNumberOfYear = '12' THEN CONVERT(int,'6') END");  
    dsv.Update();  
  
    // Add the DimGeography table  
    AddTable(dsv, connection, "DimGeography");  
  
    // Add the DimProductCategory table  
    AddTable(dsv, connection, "DimProductCategory");  
  
    // Add the DimProductSubcategory table  
    AddTable(dsv, connection, "DimProductSubcategory");  
    AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
    // Add the DimProduct table  
    AddTable(dsv, connection, "DimProduct");  
    AddComputedColumn(dsv, connection, "DimProduct", "ProductLineName", "CASE ProductLine WHEN 'M' THEN 'Mountain' WHEN 'R' THEN 'Road' WHEN 'S' THEN 'Accessory' WHEN 'T' THEN 'Touring' ELSE 'Components' END");  
    AddRelation(dsv, "DimProduct", "ProductSubcategoryKey", "DimProductSubcategory", "ProductSubcategoryKey");  
    dsv.Update();  
  
    // Add the DimCustomer table  
    AddTable(dsv, connection, "DimCustomer");  
    AddComputedColumn(dsv, connection, "DimCustomer", "FullName", "CASE WHEN MiddleName IS NULL THEN FirstName + ' ' + LastName ELSE FirstName + ' ' + MiddleName + ' ' + LastName END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "GenderDesc", "CASE WHEN Gender = 'M' THEN 'Male' ELSE 'Female' END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "MaritalStatusDesc", "CASE WHEN MaritalStatus = 'S' THEN 'Single' ELSE 'Married' END");  
    AddRelation(dsv, "DimCustomer", "GeographyKey", "DimGeography", "GeographyKey");  
  
    // Add the DimReseller table  
    AddTable(dsv, connection, "DimReseller");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderFrequencyDesc", "CASE WHEN OrderFrequency = 'A' THEN 'Annual' WHEN OrderFrequency = 'S' THEN 'Bi-Annual' ELSE 'Quarterly' END");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderMonthDesc", "CASE WHEN OrderMonth = '1' THEN 'January' WHEN OrderMonth = '2' THEN 'February' WHEN OrderMonth = '3' THEN 'March' WHEN OrderMonth = '4' THEN 'April' WHEN OrderMonth = '5' THEN 'May' WHEN OrderMonth = '6' THEN 'June' WHEN OrderMonth = '7' THEN 'July' WHEN OrderMonth = '8' THEN 'August' WHEN OrderMonth = '9' THEN 'September' WHEN OrderMonth = '10' THEN 'October' WHEN OrderMonth = '11' THEN 'November' WHEN OrderMonth = '12' THEN 'December' ELSE 'Never Ordered' END");  
  
    // Add the DimCurrency table  
    AddTable(dsv, connection, "DimCurrency");  
    dsv.Update();  
  
    // Add the DimSalesReason table  
    AddTable(dsv, connection, "DimSalesReason");  
  
    // Add the FactInternetSales table  
    AddTable(dsv, connection, "FactInternetSales");  
    AddRelation(dsv, "FactInternetSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactInternetSales", "CustomerKey", "DimCustomer", "CustomerKey");  
    AddRelation(dsv, "FactInternetSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    dsv.Update();  
  
    // Add the FactResellerSales table  
    AddTable(dsv, connection, "FactResellerSales");  
    AddRelation(dsv, "FactResellerSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactResellerSales", "ResellerKey", "DimReseller", "ResellerKey");  
    AddRelation(dsv, "FactResellerSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
  
    // Add the FactInternetSalesReason table  
    AddTable(dsv, connection, "FactInternetSalesReason");  
    AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
    dsv.Update();  
  
    // Add the FactCurrencyRate table  
    AddTable(dsv, connection, "FactCurrencyRate");  
    AddRelation(dsv, "FactCurrencyRate", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    AddRelation(dsv, "FactCurrencyRate", "TimeKey", "DimTime", "TimeKey");  
  
    #endregion  
  
    // Send the data source view definition to the server  
    dsv.Update();  
  
    return dsv;  
}  
  
static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
{  
    string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
    OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
    DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
  
    dataTable.ExtendedProperties.Add("TableType", "Table");  
    dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
    dataTable.ExtendedProperties.Add("DbTableName", tableName);  
    dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
}  
  
static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
{  
    DataSet tmpDataSet = new DataSet();  
    tmpDataSet.Locale = CultureInfo.CurrentCulture;  
    OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
        + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
        + tableName + "] WHERE 1=0", connection);  
    DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
    DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
    dataTable.Constraints.Clear();  
    dataTable.Columns.Remove(dataColumn);  
  
    dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
    dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
        expression);  
    dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
    dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
    dataColumn = null;  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
    tmpDataSet = null;  
}  
  
static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
{  
    DataColumn fkColumn  
        = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
    DataColumn pkColumn  
        = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
        + fkColumnName, pkColumn, fkColumn, true);  
}  
  
static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
{  
    DataColumn[] fkColumns = new DataColumn[2];  
    fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
    fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
    DataColumn[] pkColumns = new DataColumn[2];  
    pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
    pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
        + "_" + columnName2, pkColumns, fkColumns, true);  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](amo-classes-introduction.md)   
 [AMO 基礎類別](amo-fundamental-classes.md)   
 [邏輯架構&#40;Analysis Services-多維度資料&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件&#40;Analysis Services-多維度資料&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
