---
title: 將資料來源加入至表格式模型 (Analysis Services AMO-TOM) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 209af97f043f876f83742c599b001fded39a5f39
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="add-a-data-source-to-tabular-model-analysis-services-amo-tom"></a>將資料來源加入至表格式模型 (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
**DataSource** Microsoft.AnalysisServices.Tabular 命名空間中的類別是在資料重新整理作業期間的指定類型的表格式模型的資料來源的抽象概念和匯入資料的位置。 

可以藉由執行個體化的類別，衍生自物件將資料來源加入至表格式模型**DataSource**，然後將它新增到**DataSources**模型物件的集合。 若要變更認可到伺服器，呼叫**Model.SaveChanges()** 或**Database.Update(UpdateOptions.ExpandFull)**。 

在 SQL Server 2016 中，Analysis Services 支援資料匯入，只會從關聯式資料庫，其中的資料提供者會公開形式的資料表和資料行的資料。 因此，表格式物件模型會使用 ProviderDataSource 類別 （衍生自資料來源） 來公開此功能。 

## <a name="code-example-add-a-data-source"></a>程式碼範例： 加入資料來源 

這個範例示範如何具現化**ProviderDataSource**並將它加入至資料模型。 

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
                    server.Databases.GetNewName("Database with a Data Source Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithDataSource = new Database() 
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
                dbWithDataSource.Model = new Model() 
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
                dbWithDataSource.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = "SQL Server Data Source Example", 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithDataSource); 
                dbWithDataSource.Update(UpdateOptions.ExpandFull); 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithDataSource.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine("The data model includes the following data source definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (DataSource ds in dbWithDataSource.Model.DataSources) 
                { 
                    Console.WriteLine("\tData source name:\t\t{0}", ds.Name); 
                    Console.WriteLine("\tData source description:\t{0}", ds.Description); 
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

## <a name="next-step"></a>下一步 

在模型中，您必須設定資料來源中的來源資料行對應至模型中的目的地資料行的資料繫結。 您也必須定義資料分割，至少有一個每個資料表，儲存資料。 以下連結為您示範如何：[建立資料表、 資料分割和資料行](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md) 
