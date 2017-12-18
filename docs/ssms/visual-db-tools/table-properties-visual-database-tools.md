---
title: "資料表屬性 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.tabledesigner
- vdt.designers.properties.Table
ms.assetid: cc392987-1aab-45f5-b5af-a26be53409bf
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7dc7692744a8f1b194e10591106d43d0f8aa938d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="table-properties-visual-database-tools"></a>資料表屬性 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 當您在資料表設計工具中按一下滑鼠右鍵並選取 [屬性] 時，這些屬性便會出現在 [屬性] 視窗中。 已選取資料表時，您可以在 [屬性] 視窗中編輯這些屬性 (除非另有附註)。  
  
> [!NOTE]  
> 如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
## <a name="show-table-properties-in-table-designer"></a>在資料表設計師中顯示資料表屬性  
  
> [!NOTE]  
> 此主題中的屬性，是依類別目錄的順序排列，而非依字母排列。  
  
**識別類別目錄**  
展開以顯示 **名稱**、 **說明**及 **結構描述**的屬性。  
  
**名稱**  
顯示資料表的名稱。 若要編輯名稱，請在文字方塊中輸入。  
  
> [!CAUTION]  
> 如果現有的查詢、檢視、使用者自訂函數、預存程序或程式參考此資料表，則名稱修改將使這些物件失效。  
  
**資料庫名稱**  
顯示選取資料表的資料來源名稱。  
  
**說明**  
顯示選取資料表的描述。 若要查看或編輯整個描述，請按一下 [描述]，再按屬性右邊的省略符號 **(…)** 。  
  
**結構描述**  
顯示此資料表所屬結構描述的名稱 (只適用於 Microsoft SQL Server)。  
  
**伺服器名稱**  
顯示資料來源的伺服器名稱。  
  
**資料表設計工具類別目錄**  
展開以顯示 **Identity Column**、 **Is Indexable**及 **Is Replicated**的屬性。  
  
**Identity Column**  
顯示做為資料表識別欄位的資料行。 若要變更識別欄位，請從下拉式清單中選擇。 清單中只會顯示數字資料類型的資料行。  
  
**Is Indexable**  
顯示是否可對資料表進行索引。 如果資料表不可索引，可能是因為您不是資料表擁有人，或是因為資料表包含具有 text、ntext 或 image 等資料類型的資料行。  
  
**Is Replicated**  
顯示是否已在其他位置複寫資料表。  
  
**規則資料空間規格分類**  
展開以顯示 **(資料空間類型)**、 **檔案群組或資料分割配置名稱**及 **資料分割資料行清單**的屬性。  
  
**(資料空間類型)**  
顯示此資料表是否使用檔案群組或資料分割配置加以儲存。  
  
**檔案群組或資料分割配置名稱**  
顯示檔案群組或資料分割配置的名稱。  
  
**資料分割資料行清單**  
提供 **資料分割資料行清單** 的存取權。  
  
**資料列 GUID 資料行**  
顯示 Microsoft SQL Server 用來做為資料表之 ROWGUID 資料行的資料行。 若要變更 ROWGUID 資料列，請從下拉式清單中選擇 (只適用於 SQL Server 7.0 (含) 以後版本)。  
  
**Text/Image 檔案群組**  
提供下拉式清單，供您選擇具有 text 或 image 資料類型之資料行的檔案群組。 如果資料表是以資料分割配置加以儲存，請將此欄位留白。  
  
## <a name="see-also"></a>另請參閱  
[設計資料表 (Visual Database Tools)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  
