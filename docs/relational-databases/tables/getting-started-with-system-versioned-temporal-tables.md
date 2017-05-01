---
title: "開始使用系統建立版本的時態表 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0318f2a574bcdb2f02016fc6d865252deb6fef4a
ms.lasthandoff: 04/11/2017

---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>開始使用系統建立版本的時態表
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  根據您的案例，您可以建立新的系統建立版本的時態表，或修改現有的時態表，方法是將 temporal 屬性加入現有的資料表結構描述。   
時態表中的資料修改時，系統就會建置應用程式和使用者看不到的版本歷程記錄。 如此一來，使用系統建立版本的時態表不需要對資料表的修改方法，或查詢資料的最新 (實際) 狀態的方式進行任何變更。   
除了一般資料操作語言 (DML) 和查詢，Temporal 也提供方便且簡單的方式，透過擴充的 Transact-SQL 語法，從資料歷程記錄中取得見解。   
每個系統建立版本的資料表中有一個指派的歷程記錄資料表，但是使用者完全看不到，除非他們想要藉由建立額外的索引，或選擇不同的儲存體選項，最佳化工作負載效能或儲存體使用量。    
下列圖表描述使用系統建立版本的時態表的一般工作流程︰   
![開始使用時態表](../../relational-databases/tables/media/getting-started-with-temporal.png "Getting Started with Temporal")  
  
 本主題分成以下 5 個子主題：  
  
-   [建立系統建立版本的時態表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
-   [修改系統建立版本時態表中的資料](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
-   [查詢系統建立版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
-   [變更系統建立版本時態表的結構描述](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
-   [停止系統版本設定時態表上的系統版本設定功能](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Getting%20Started%20with%20System-Versioned%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>另請參閱  
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [對時態表進行資料分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [時態表考量與限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [時態表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

