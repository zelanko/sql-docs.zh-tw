---
title: 資料庫標記法（表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 16a233fb-f83b-4ca1-acb5-6186eca0a62c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 377b85c22d1c6da9f5296d6ad57a86028e022785
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62757814"
---
# <a name="database-representationtabular"></a>資料庫表示法 (表格式)
  在表格式模式下，資料庫是表格式模型中所有物件的容器。  
  
## <a name="database-representation"></a>資料庫表示法  
 資料庫是形成表格式模型之所有物件所在的地方。 開發人員會在資料庫這個容器內尋找物件，諸如連接、資料表、角色等。  
  
### <a name="database-in-amo"></a>AMO 中的資料庫  
 當您使用 AMO 管理表格式模型資料庫時，AMO 中的 <xref:Microsoft.AnalysisServices.Database> 物件與表格式模型中的資料庫邏輯物件會有一對一的相符關係。  
  
> [!NOTE]  
>  為了要能夠存取資料庫物件，使用者需要在 AMO 中擁有伺服器物件的存取權並加以連接。  
  
### <a name="database-in-adomdnet"></a>ADOMD.Net 中的資料庫  
 當您使用 ADOMD 參照及查詢表格式模型資料庫時，將透過 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件取得對特定資料庫的連接。  
  
 您可以使用以下程式碼片段直接連接至特定資料庫：  
  
```csharp  
using ADOMD = Microsoft.AnalysisServices.AdomdClient;  
...  
   ADOMD.AdomdConnection currrentCnx = new ADOMD.AdomdConnection("Data Source=<<server\instance>>;Catalog=<<database>>");  
   currrentCnx.Open();  
...  
  
```  
  
 此外，您也可透過現有尚未關閉的連接物件，將目前的資料庫變更為另一個資料庫，如以下程式碼片段所示：  
  
```csharp  
currentCnx.ChangeDatabase("myOtherDatabase");  
  
```  
  
## <a name="database-in-amo"></a>AMO 中的資料庫  
 當您要使用 AMO 管理資料庫物件時，請從 <xref:Microsoft.AnalysisServices.Server> 物件開始著手。 接著在資料庫集合中搜尋您的資料庫，或透過加入資料庫至該集合的方式建立新的資料庫。  
  
 下列程式碼片段顯示在檢查資料庫不存在之後，連接到伺服器並建立空資料庫的步驟：  
  
```  
  
AMO.Server CurrentServer = new AMO.Server();  
try  
{  
    CurrentServer.Connect(currentServerName);  
}  
catch (Exception cnxException)  
{  
    MessageBox.Show(string.Format("Error while trying to connect to server: [{0}]\nError message: {1}", currentServerName, cnxException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    return;  
}  
newDatabaseName = DatabaseName.Text;  
if (CurrentServer.Databases.Contains(newDatabaseName))  
{  
    return;  
}  
try  
{  
    AMO.Database newDatabase = CurrentServer.Databases.Add(newDatabaseName);  
  
    CurrentServer.Update();  
}  
catch (Exception createDBxc)  
{  
    MessageBox.Show(String.Format("Database [{0}] couldn't be created.\n{1}", newDatabaseName, createDBxc.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    newDatabaseAvailable = false;  
}  
  
```  
  
 若想實際了解如何使用 AMO 建立及操作資料庫表示法，請參閱「表格式 AMO 2012」範例的原始程式碼，特別要檢查以下的原始程式檔：Database.cs。 提供此範例程式碼的用意只是為了支援這裡所說明的邏輯概念，您不應將其用於生產環境。  
  
  
