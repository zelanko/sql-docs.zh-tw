---
title: Alter 命令 (TMSL) |Microsoft 文件
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 8bdc49f1-209e-4055-be19-c83862b81efa
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a28e96ff40a83b3994e0af143a17e21ae8111cf5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="alter-command-tmsl"></a>Alter 命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  改變現有的物件，但不是及其子系，在以表格式模式的 Analysis Services 執行個體上。  如果物件不存在，命令就會引發錯誤。  
  
 使用**Alter**命令目標的更新，例如在資料表上設定屬性，而不需要指定所有的資料行。 這個命令是類似於**CreateOrReplace**，但不會提供完整物件定義的需求。  
  
 物件都有讀寫屬性，如果您指定一個讀 / 寫屬性，您必須指定所有它們使用新的或現有的值。 您可以使用 AMO PowerShell 來取得屬性清單。 
  
## <a name="request"></a>要求  
 **Alter**並沒有任何屬性。 輸入包含要改變，後面接著已修改的物件定義的物件。  
  
 下列範例說明語法變更磁碟分割物件上的屬性。 物件路徑建立哪個資料分割物件是要改變透過父物件的名稱 / 值組。 第二個輸入是指定新的屬性值的資料分割物件。  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "\<database-name>",   
      "table": "\<table-name>",   
      "partition": "\<partition-name>"   
    },   
    "partition": {   
      "name": "\<new-partition-name>",   
       . . .  << other properties   
    }   
  }   
}   
```  
  
 要求的結構會根據物件而異。 **Alter**可以搭配任何下列物件：  
  
 [資料庫物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)重新命名資料庫。  
  
```  
"alter": {   
    "object": {   
      "database": "\<database-name>"  
    },   
    "database": {   
      "name": "\<new-database-name>",   
    }   
  }   
```  
  
 [資料來源物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)重新命名連線，也就是資料庫的子物件。  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "dataSource":"SqlServer localhost AdventureworksDW2016"  
      },  
      "dataSource":{   
         "name":"A new connection name"  
      }  
   }  
}  
```  
  
 [Tables 物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)看到**範例 1**下方。  
  
 [資料分割物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)看到**範例 2**下方。  
  
 [角色物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)變更角色物件上的屬性。  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "role":"DataReader"  
      },  
      "role":{   
         "name":"New Name"  
      }  
   }  
}  
```  
  
## <a name="response"></a>回應  
 當命令執行成功，則傳回空的結果。 否則，傳回 XMLA 例外狀況。  
  
## <a name="examples"></a>範例  
 下列範例示範指令碼，您可以在 Management Studio 中的 XMLA 視窗中執行，或使用做為輸入中[Invoke-ascmd 指令程式](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)AMO PowerShell 中。  
  
 **範例 1** -此指令碼變更的資料表上的 [名稱] 屬性。  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "AdventureWorksDW2016",   
      "table": "DimDate"  
    },   
    "table": {   
      "name": "DimDate2"  
    }   
  }   
}  
```  
  
 假設本機具名執行個體 （執行個體名稱為 「 表格式 」） 和 JSON 檔案，含有 alter 指令碼，此命令從 DimDate 變更資料表名稱為 DimDate2:  
  
 `invoke-ascmd -inputfile '\\my-computer\my-shared-folder\altertablename.json' -server 'localhost\Tabular'`  
  
 **範例 2** -此指令碼會重新命名分割區，例如在目前的年份時前一年的年度結束。 請確定指定的所有屬性。 如果您離開**來源**未指定，它可能會中斷所有現有的資料分割定義。  
  
 除非您要建立、 取代或改變資料來源物件本身，在您的指令碼 （例如在下列資料分割的指令碼） 中參考的任何資料來源必須是現有**DataSource**模型中的物件。 如果您需要變更的資料來源，這樣做為個別的步驟。  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "InternetSales",   
      "table": "DimDate",  
      "partition": "CurrentYear"  
    },   
    "partition": {   
      "name": "Year2009",  
       "source": {  
             "query":  "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] WHERE [dbo].[DimDate].CalendarYear = 2009",  
              "dataSource": "SqlServer localhost AdventureworksDW2016"  
        }  
    }   
  }   
}  
```  
  
## <a name="usage-endpoints"></a>使用方式 （端點）  
 這個命令項目用在陳述式的[Execute Method &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)呼叫透過 XMLA 端點，以下列方式公開：  
  
-   以 XMLA 視窗中 SQL Server Management Studio (SSMS)  
  
-   為輸入檔案**叫用 ascmd** PowerShell cmdlet  
  
-   做為輸入到 SSIS 工作或 SQL Server Agent 作業  
  
 您無法從 SSMS 產生現成的指令碼，此命令。 相反地，您可以開始使用範例，或撰寫您自己。  
  
 [ \[MS-SSAS T\]: QL Server Analysis Services 表格式 （SQL Server 技術通訊協定）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文件包含區段 3.1.5.2.2 描述結構的 JSON 表格式中繼資料命令和物件。 目前，該文件涵蓋命令和功能尚未實作用於 TMSL 指令碼。 請參閱主題 ([表格式模型指令碼語言&#40;TMSL&#41;參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) 以釐清支援的項目。  

## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
