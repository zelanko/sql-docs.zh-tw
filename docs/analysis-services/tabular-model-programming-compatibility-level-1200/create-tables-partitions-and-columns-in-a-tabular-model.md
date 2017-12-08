---
title: "表格式模型中建立資料表、 資料分割和資料行 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: cf0e4791-ad3b-41a8-81ce-509d4cf223f8
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ecf8c233177b283c5dc3a5601a267bdfa0c8a10f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="create-tables-partitions-and-columns-in-a-tabular-model"></a>表格式模型中建立資料表、 資料分割和資料行

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在表格式模型中，資料表是由資料列和資料行所組成。 資料列會組織成資料分割，以支援累加式的資料重新整理。 表格式解決方案可支援幾種類型的資料表，根據資料來自何處：  

* 一般的資料表，從關聯式資料來源，此資料提供者透過產生資料。 

* 推入的資料表，其中資料 「 推入 」 的資料表以程式設計的方式。 

* 導出的資料表資料的來源參考另一個物件，其資料模型中的 DAX 運算式。  

在下列程式碼範例中，我們會定義一般資料表。 

## <a name="required-elements"></a>必要的項目 

資料表必須有至少一個資料分割。 一般資料表也必須定義至少一個資料行。 

每個資料分割必須擁有指定的資料來源的來源，但您可以將來源為 null。 一般而言，來源是定義在相關資料庫的查詢語言中的資料配量的查詢運算式。 

## <a name="code-example-create-a-table-column-parition"></a>程式碼範例： 建立資料表、 資料行、 資料分割

資料表表示資料表中的類別 （Microsoft.AnalysisServices.Tabular 命名空間）。 

在下列範例中，我們會定義一般資料表有一個連結至關聯式資料來源和幾個一般的資料行的資料分割。 我們也會將變更提交至伺服器，並觸發程序會將資料帶入模型的資料重新整理。 當您要從 SQL Server 關聯式資料庫的資料載入表格式解決方案時，這代表最常見的案例。 


```
using System; 
using Microsoft.AnalysisServices; 
using Microsoft.AnalysisServices.Tabular; 
 
namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 
 
            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 
 
                // 
                // Generate a new database name and use GetNewName 
                // to ensure the database name is unique. 
                // 
                string newDatabaseName = 
                    server.Databases.GetNewName("Database with a Table Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithTable = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.Model object to the 
                // database, which acts as a root for all other Tabular metadata objects. 
                // 
                dbWithTable.Model = new Model() 
                { 
                    Name = "Tabular Data Model", 
                    Description = "A Tabular data model at the 1200 compatibility level." 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.ProviderDataSource object 
                // to the data Model object created in the previous step. The connection 
                // string of the data source object in this example  
                // points to an instance of the AdventureWorks2014 SQL Server database. 
                // 
                string dataSourceName = "SQL Server Data Source Example"; 
                dbWithTable.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = dataSourceName, 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                //  
                // Add a table called Individual Customers to the data model 
                // with a partition that points to a [Sales].[vIndividualCustomer] view 
                // in the underlying data source. 
                // 
                dbWithTable.Model.Tables.Add(new Table() 
                { 
                    Name = dbWithTable.Model.Tables.GetNewName("Individual Customers"), 
                    Description = "Individual customers (names and email addresses) that purchase Adventure Works Cycles products online.", 
                    Partitions = { 
                        // 
                        // Create a single partition with a QueryPartitionSource for a query 
                        // that imports all customer rows from the underlying data source. 
                        // 
                        new Partition() { 
                            Name = "All Customers", 
                            Source = new QueryPartitionSource() { 
                                DataSource = dbWithTable.Model.DataSources[dataSourceName], 
                                Query = @"SELECT   [FirstName] 
                                                    ,[MiddleName] 
                                                    ,[LastName] 
                                                    ,[PhoneNumber]  
                                                    ,[EmailAddress] 
                                                    ,[City] 
                                        FROM [Sales].[vIndividualCustomer]", 
                            } 
                        } 
                    }, 
                    Columns = 
                    { 
                        // 
                       // DataColumn objects refer to regular table columns.  
                        // Each DataColumn object corresponds to a column in the underlying data source query. 
                        // 
                        new DataColumn() { 
                            Name = "FirstName", 
                            DataType = DataType.String, 
                            SourceColumn = "FirstName", 
                        }, 
                        new DataColumn() { 
                            Name = "MiddleName", 
                            DataType = DataType.String, 
                            SourceColumn = "MiddleName", 
                        }, 
                        new DataColumn() { 
                            Name = "LastName", 
                            DataType = DataType.String, 
                            SourceColumn = "LastName", 
                        }, 
                        new DataColumn() { 
                            Name = "PhoneNumber", 
                            DataType = DataType.String, 
                            SourceColumn = "PhoneNumber", 
                        }, 
                        new DataColumn() { 
                            Name = "EmailAddress", 
                            DataType = DataType.String, 
                            SourceColumn = "EmailAddress", 
                        }, 
                        new DataColumn() { 
                            Name = "City", 
                            DataType = DataType.String, 
                            SourceColumn = "City", 
                        }, 
                    } 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithTable); 
 
                //  
                // Request a full refresh to import the data from the data source and 
                // and perform any necessary recalculations. 
                // The refresh operation will be performed with the next 
                // invocation of Model.SaveChanges() or Database.Update(UpdateOptions.ExpandFull). 
                dbWithTable.Model.RequestRefresh(Microsoft.AnalysisServices.Tabular.RefreshType.Full); 
                dbWithTable.Update(UpdateOptions.ExpandFull); 
 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithTable.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
 
                Console.WriteLine("The data model includes the following table definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (Table tbl in dbWithTable.Model.Tables) 
                { 
                    Console.WriteLine("\tTable name:\t\t{0}", tbl.Name); 
                    Console.WriteLine("\ttbl description:\t{0}", tbl.Description); 
                } 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="partitions-in-a-table"></a>在資料表中的資料分割 

資料分割都由**分割**類別 （在 Microsoft.AnalysisServices.Tabular 命名空間）。 **分割**類別會公開**來源**屬性 P**artitionSource**類型，可提供抽象概念，透過不同的方法擷取資料資料分割。 A**分割**執行個體可以有**來源**屬性為 null，表示資料推送至資料分割時所傳送到伺服器的資料區塊的一部分推入 Analysis Services 所公開的資料 API. 在 SQL Server 2016， **PartitionSource**類別有兩個衍生的類別，代表將資料繫結至資料分割的方式： **QueryPartitionSource**和**CalculatedPartitionSource**. 

## <a name="columns-in-a-table"></a>資料表中的資料行 

資料行都由數個類別衍生自基底**資料行**（在 Microsoft.AnalysisServices.Tabular 命名空間） 的類別： 

* **DataColumn** （適用於一般資料表中的一般資料行）
* **CalculatedColumn** （適用於 DAX 運算式所支援的資料行）
* **CalculatedTableColumn** （適用於導出資料表中的一般資料行）
* **RowNumberColumn** （SSAS 所建立的每個資料表的資料行的特殊類型）。 

## <a name="row-numbers-in-a-table"></a>在資料表中的資料列號碼 

每個**資料表**在伺服器上的物件具有**RowNumberColumn**基於索引目的使用。 您無法建立或明確地將它加入。 當您儲存或更新物件時，會自動建立資料行： 

* **db。SaveChanges** 

* **db。Update(ExpandFull)** 

呼叫其中一個方法時，伺服器將資料列號碼資料行自動建立，這將會顯示為**RowNumberColumn**資料表的資料行集合。 

## <a name="calculated-tables"></a>計算資料表 

導出的資料表被來自 repurposes 現有模型中的資料結構的資料-單行繫結的 DAX 運算式。 若要以程式設計方式建立的導出的資料表，執行下列作業： 

* 建立一般**資料表**。 

* 將分割區來源類型為**CalculatedPartitionSource**、 來源所在的 DAX 運算式。 資料分割的來源是導出資料表的差異一般資料表。 

當您將變更儲存至伺服器時，伺服器將傳回的清單推斷**CalculatedTableColumns** （導出資料表所組成的導出的資料表資料行），透過資料表的資料行集合中看見。 

## <a name="next-steps"></a>後續的步驟

檢閱用於 TOM 中處理例外狀況的類別： [TOM 中的錯誤處理](../../analysis-services/tabular-model-programming-compatibility-level-1200/handling-errors-in-the-tom-api-analysis-services-amo-tom.md)
  
