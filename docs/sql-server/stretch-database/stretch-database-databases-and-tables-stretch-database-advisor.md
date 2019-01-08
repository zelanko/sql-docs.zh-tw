---
title: 識別 Stretch Database 的資料庫和資料表 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2017
ms.prod: sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9adc861d24713204c819787dce3b79a38230c08c
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2018
ms.locfileid: "53597139"
---
# <a name="identify-databases-and-tables-for-stretch-database-with-data-migration-assistant"></a>使用 Data Migration Assistant 識別適用於 Stretch Database 的資料庫和資料表
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  若要識別適用於 Stretch Database 的資料庫和資料表，以及潛在的封鎖問題，請下載並執行 Microsoft Data Migration Assistant。
  
## <a name="get-data-migration-assistant"></a>取得 Data Migration Assistant
 從 [這裡](https://www.microsoft.com/download/details.aspx?id=53595)下載並安裝 Data Migration Assistant。 SQL Server 安裝媒體未隨附此工具。  
  
## <a name="run-data-migration-assistant"></a>執行 Data Migration Assistant  
  
1.  執行 Microsoft Data Migration Assistant。  

2.  建立類型為 [Assessment] (評量) 的新專案並指定名稱。

3.  選取 **SQL Server** 同時作為 [Source server type ] (來源伺服器類型) 和 [Target server type] (目標伺服器類型)。

4.  選取 [建立]。 

5. 在 [Options] (選項) 頁面上 (步驟 1)，選取 [New features recommendation] (新增功能建議)。 (選擇性) 清除 [Compatibility issues] (相容性問題) 的選取。

6.  在 [Select sources] (選取來源) 頁面上 (步驟 2)，連線到一部伺服器並選取一個資料庫，然後選取 [Add ] (新增)。

7.  選取 [Start Assessment] (啟動評量)。

## <a name="review-the-results"></a>檢閱結果  
  
1.  當分析完成時，在 [Review results] (檢閱結果)  頁面上 (步驟 3)，選取 [Feature recommendations] (功能建議) 選項，然後選取 [Storage] (儲存體) 索引標籤。

2.  檢閱 Stretch Database 的相關建議。 每個建議會列出 Stretch Database 可能適用的資料表，以及任何潛在的封鎖問題。

## <a name="historical-note"></a>歷史備註
Stretch Database Advisor 之前是 SQL Server 2016 Upgrade Advisor 的一個元件。 在當時，您必須另外選取並執行 Stretch Database Advisor。

發行 Data Migration Assistant 以取代並擴充 Upgrade Advisor 之後，Stretch Database Advisor 的功能會併入這項新工具。 您不需要選取任何選項，即可取得 Stretch Database 的相關建議。 當您在 Data Migration Assistant 中執行評量時，Stretch Database 的相關結果會出現在 [Feature recommendations ] (功能建議) 的 [Storage] (儲存體) 索引標籤中。
  
## <a name="next-step"></a>下一步  
 啟用 Stretch Database。  
  
-   若要在 **資料庫**上啟用 Stretch Database，請參閱 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
-   若要在另一個 **資料表**上啟用 Stretch Database，而且已在資料庫上啟用 Stretch，則請參閱 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。 
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database 的限制](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [為資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
