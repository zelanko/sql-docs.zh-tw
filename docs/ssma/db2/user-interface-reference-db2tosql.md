---
title: 使用者介面參考 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 98ecc4ff-9416-48a2-af0f-86852cf69dab
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dfb8a549433d3f807c15e15468f95cf4d2289794
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979801"
---
# <a name="user-interface-reference-db2tosql"></a>使用者介面參考 (DB2ToSQL)
本節包含說明主題[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) for DB2。  
  
## <a name="in-this-section"></a>本節內容  
下表列出的 SSMA 對話方塊：  
  
|||  
|-|-|  
|主題|描述|  
|[進階物件選取項目&#40;DB2ToSQL&#41;](../../ssma/db2/advanced-object-selection-db2tosql.md)|使用**進階物件選取**對話方塊來尋找資料庫物件所使用的篩選準則，然後選取或清除這些物件。|  
|[評定報告&#40;DB2ToSQL&#41;](../../ssma/db2/assessment-report-db2tosql.md)|若要檢視的 DB2 物件要轉換的結果使用評定報告[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，以及評估要移轉的複雜度與時間[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[連接至 DB2 資料庫&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)|使用**連接到 DB2**對話方塊連接到您想要移轉的 DB2 資料庫。|  
|[連接到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/connect-to-sql-server-db2tosql.md)|使用**連接到 SQL Server**對話方塊中，連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]至您想要移轉。|  
|[資料移轉報告&#40;DB2ToSQL&#41;](../../ssma/db2/data-migration-report-db2tosql.md)|顯示的結果將資料從 DB2，以便移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[資料移轉設定](http://msdn.microsoft.com/573e673e-a194-4cb2-9aba-aaac6e1a225c)|使用**擴充資料移轉設定**撰寫自訂查詢的資料移轉 索引標籤。|  
|[編輯類型對應&#40;DB2ToSQL&#41;](../../ssma/db2/edit-type-mapping-db2tosql.md)|使用**新的類型對應**或是**編輯類型對應**對話方塊來建立或修改的來源和目標資料庫和資料庫物件之間的資料類型對應。|  
|[全域設定&#40;編輯器&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/global-settings-editor-db2tosql.md)|使用編輯器頁面**全域設定**對話方塊來設定程式碼編輯器選項。|  
|[全域設定&#40;對話方塊&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/global-settings-dialogs-db2tosql.md)|使用對話方塊頁面**全域設定**對話方塊來設定預設的對話方塊和警告設定。|  
|[全域設定&#40;記錄&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/global-settings-logging-db2tosql.md)|使用 [記錄] 頁面的**全域設定**對話方塊來設定記錄。|  
|[全域設定&#40;輸出視窗&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/global-settings-output-window-db2tosql.md)|使用**全域設定**對話方塊，即可設定 SSMA for DB2 使用者介面的喜好設定。|  
|[新的專案&#40;DB2ToSQL&#41;](../../ssma/db2/new-project-db2tosql.md)|使用**新的專案**對話方塊來建立新的 SSMA for DB2 的專案。|  
|[專案設定&#40;轉換&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)|使用 [轉換] 頁面**專案設定**對話方塊來指定如何 SSMA for DB2 轉換函式和全域變數。|  
|[專案設定&#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)|使用 GUI 頁面**專案設定**對話方塊來指定在顯示的資料量**資料** 索引標籤。|  
|[專案設定&#40;移轉&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)|使用 [移轉] 頁面**專案設定**對話方塊，即可自訂如何 SSMA for DB2 將資料從移轉到 DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[專案設定&#40;同步處理&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)|使用同步處理頁面**專案設定**對話方塊，自訂 SSMA for DB2 會建立或改變的方式移轉的資料庫物件中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[專案設定&#40;載入系統物件&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)|使用 [載入系統物件] 頁面**專案設定**對話方塊來指定哪一個 DB2 系統物件 SSMA 會將轉換和載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|[專案設定&#40;類型對應&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)|使用型別對應頁面**專案設定**對話方塊來指定所有資料庫和資料庫物件的預設型別對應的 SSMA for DB2 的專案中。|  
|[從資料庫重新整理&#40;DB2ToSQL&#41;](../../ssma/db2/refresh-from-database-db2tosql.md)|使用**從資料庫重新整理**對話方塊，即可選取要重新整理從 DB2 資料庫物件。|  
|[儲存中繼資料&#40;DB2ToSQL&#41;](../../ssma/db2/save-metadata-db2tosql.md)|**儲存中繼資料**儲存遺失中繼資料的專案時，對話方塊隨即出現。|  
  
## <a name="see-also"></a>另請參閱  
[開始使用 SSMA for DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
[移轉的 DB2 資料庫到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
