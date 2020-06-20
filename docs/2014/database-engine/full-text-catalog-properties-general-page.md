---
title: 全文檢索目錄屬性（一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.general.f1
ms.assetid: d1f66762-2d40-4f24-b635-a417d22ee79a
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e2411daea2d4b1c4028e9ed0b3143762f2db592
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933019"
---
# <a name="full-text-catalog-properties-general-page"></a>全文檢索目錄屬性 (一般頁面)
  本章節會顯示在 **[全文檢索目錄屬性]** 對話方塊的 **[一般]** 頁面上，可以使用的選項和功能。  
  
> [!NOTE]  
>  對於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 資料庫而言，全文檢索目錄是參考一組全文檢索索引的邏輯概念。 全文檢索目錄是不屬於任何檔案群組的虛擬物件。  
  
## <a name="options"></a>選項。  
  
### <a name="properties"></a>[內容]  
 **預設目錄**  
 顯示目錄是否為資料庫的預設目錄。  
  
 **母體擴展狀態**  
 指出目錄的狀態。 可能的值包括：  
  
-   **閒置**  
  
-   **搜耙進行中**  
  
-   **已暫停**  
  
-   **調整執行速度**  
  
-   **待**  
  
-   **關機**  
  
-   **遞增擴展進行中**  
  
-   **正在建立索引**  
  
-   **磁片已滿已暫停**  
  
-   **Change tracking**  
  
 **項目計數**  
 顯示目錄中全文檢索項目的數目。  
  
 **目錄大小**  
 顯示全文檢索目錄的大小，以 MB 為單位。  
  
 **名稱**  
 全文檢索目錄的名稱。  
  
 **區分重音**  
 查看或修改類別目錄是否區分變音符號，例如波狀 **~** 符號（）、銳角、重音符號（**́**），或母音（**？**）。 有效值為：  
  
-   **否**  
  
-   **是**  
  
-   如需有關變音符號的詳細資訊，請參閱 Merriam-Webster 字典中的[變音符號](https://www.merriam-webster.com/dictionary/diacritic)。  
  
 **上次母體擴展日期**  
 顯示目錄上次擴展的日期。  
  
 **擁有者**  
 全文檢索目錄的擁有者。  
  
 **唯一索引鍵計數**  
 構成目錄的全文檢索索引之唯一字的數目。  
  
### <a name="catalog-action"></a>目錄動作  
  
|||  
|-|-|  
|**None**|不會執行 **最佳化目錄**、 **重建目錄**，或 **重新擴展目錄** 等作業。|  
|**最佳化目錄**|最佳化目錄的空間利用，並改善查詢的效能。 它還會改善搜尋結果之次序相關性的精確性。<br /><br /> 此動作會執行 ALTER FULLTEXT CATALOG *catalog_name* REORGANIZE。|  
|**重建目錄**|刪除並重建全文檢索目錄。 如果已變更基礎的目錄屬性 (例如區分腔調字)，就必須執行此項作業。<br /><br /> 為了使重建能順利完成，全文檢索目錄所存在的檔案群組必須在線上，或者可供讀寫。 重建之後，就會重新擴展全文檢索的索引。<br /><br /> 此動作會執行 ALTER FULLTEXT CATALOG *catalog_name* REBUILD。|  
|**重新擴展目錄**|用資料最近的變更來更新目錄。 此選項不需要關閉目錄。|  
  
## <a name="see-also"></a>另請參閱  
 [擴展全文檢索索引](../relational-databases/indexes/indexes.md)  
  
  
