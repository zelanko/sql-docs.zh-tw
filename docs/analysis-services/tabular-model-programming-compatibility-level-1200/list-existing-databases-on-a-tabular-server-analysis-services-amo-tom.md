---
title: "列出現有的資料庫，在表格式伺服器 (Analysis Services AMO-TOM) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ab5eb4b8-6254-442d-a42e-2372c346d260
caps.latest.revision: "2"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 79563e4a6bcbcbf5aa52e903b81cb9c3fcb9639c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="list-existing-databases-on-a-tabular-server-analysis-services-amo-tom"></a>列出在表格式伺服器 (Analysis Services AMO-TOM) 上的現有資料庫
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]當您有**伺服器**物件連接到 Analysis Services 執行個體，您可以反覆查看**Server.Databases**列出分析會服務執行個體所裝載的所有資料庫的集合。 

**Server.Databases**集合會包含一個**資料庫**裝載在伺服器上，不論伺服器模式 （Multidimensional 或 Tabular） 或資料庫類型 （多維度，每個資料庫物件表格式的前 1200 或表格式 1200年或更高版本）。 

您可以檢查的資料庫，透過類型**Database.StorageEngineUsed**屬性。  

表格式 1200年 （含） 以上的資料庫將會傳回非 null **Database.Model**屬性可存取所有表格式中繼資料物件： 資料表、 資料行、 關聯性等等。  

多維度或表格式 1103年和其下 Database.Model 屬性會是 null。 在此情況下，非表格式中繼資料將可在多維度屬性 （例如 Database.Cubes 和 Database.Dimensions），但這些屬性，才會顯示由 Microsoft.AnalysisServices.Database 類別 （從 AMO)，不是由Microsoft.AnalysisServices.Tabular.Database （適用於 TOM)。 如需有關要使用哪一個資料庫類別的詳細資訊，請參閱[安裝、 散佈及參考 TOM 用戶端程式庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)。

Database.StorageEngineUsed 設為 TabularMetadata，除非您將無法使用的表格式命名空間中的其他類別，來存取或操作模型樹狀結構。 

下表摘要說明預期的行為，當您連接到伺服器或資料庫伺服器或資料庫上使用 Microsoft.AnalysisServices.Tabular 類別。 

mode | Database.model | Database.StorageEngineUsed
-----|----------------|---------------------------
表格式 1200，1400年 | 傳回模型的名稱| StorageEngineUsed.TabularMetadata 
1103 表格式 1100年、 1050年 | 會傳回 null | StorageEngineUsed.InMemory 
多維度 | 會傳回 null | StorageEngineUsed.Traditional 

## <a name="code-example-list-existing-databases"></a>程式碼範例： 列出現有的資料庫

下列程式碼說明如何連接到伺服器所裝載的伺服器和清單資料庫。 

```
using System; using Microsoft.AnalysisServices; 
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
                // List common properties for the databases on the server. 
                // 
                foreach (Database db in server.Databases) 
                { 
                    Console.WriteLine("Properties for database {0}:", db.Name); 
                    Console.ForegroundColor = ConsoleColor.Yellow; 
                    Console.WriteLine("Database ID:\t\t\t{0}", db.ID); 
                    Console.WriteLine("Database compatibility level:\t{0}", db.CompatibilityLevel); 
                    Console.WriteLine("Database collation:\t\t{0}", db.Collation); 
                    Console.WriteLine("Database created timestamp:\t{0}", db.CreatedTimestamp); 
                    Console.WriteLine("Database language ID:\t\t{0}", db.Language); 
                    Console.WriteLine("Database model type:\t\t{0}", db.ModelType); 
                    Console.WriteLine("Database state:\t\t\t{0}", db.State); 
                    Console.ResetColor(); 
                    Console.WriteLine(); 
                } 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```


## <a name="get-an-item-from-a-database"></a>從資料庫取得的項目 

下列程式碼片段會示範如何取得表格式或從資料庫的資料行。 


```
var db = srv.Databases.GetByName("abc"); 

Column c1 = db.Model.Tables["foo"].Columns["bar"]; 
if (c1.ObjectType == ObjectType.Column) // always true 

MetadataObject obj; 

switch(obj.ObjectType) 
{ 
 case ObjectType.Table: 
  var t1 = (Table)obj; 
  break; 
} 
```

## <a name="next-steps"></a>後續的步驟

了解如何[建立及部署的空白資料庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)使用 TOM API。

