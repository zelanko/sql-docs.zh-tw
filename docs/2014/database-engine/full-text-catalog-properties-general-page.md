---
title: 全文檢索目錄屬性 （一般頁面） |Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.general.f1
ms.assetid: d1f66762-2d40-4f24-b635-a417d22ee79a
caps.latest.revision: 34
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fc774b0dfd87ae4f63e9332dd6813d92f79e4a5c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136471"
---
# <a name="full-text-catalog-properties-general-page"></a>全文檢索目錄屬性 (一般頁面)
  本章節會顯示在 **[全文檢索目錄屬性]** 對話方塊的 **[一般]** 頁面上，可以使用的選項和功能。  
  
> [!NOTE]  
>  如[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]資料庫中，全文檢索目錄是參考一組全文檢索索引的邏輯概念。 全文檢索目錄是不屬於任何檔案群組的虛擬物件。  
  
## <a name="options"></a>選項。  
  
### <a name="properties"></a>屬性  
 **預設目錄**  
 顯示目錄是否為資料庫的預設目錄。  
  
 **母體擴展狀態**  
 指出目錄的狀態。 可能的值為：  
  
-   **閒置**  
  
-   **搜耙進行中**  
  
-   **已暫停**  
  
-   **節流**  
  
-   **復原**  
  
-   **關機**  
  
-   **累加母體擴展正在進行中**  
  
-   **正在建立索引**  
  
-   **磁碟已滿 — 已暫停**  
  
-   **Change tracking**  
  
 **項目計數**  
 顯示目錄中全文檢索項目的數目。  
  
 **類別目錄大小**  
 顯示全文檢索目錄的大小，以 MB 為單位。  
  
 **名稱**  
 全文檢索目錄的名稱。  
  
 **區分腔調字**  
 檢視或修改目錄是否會區分變音符號，例如波狀符號 (**~**)、尖重音符號 (**´**) 或母音變化 (**¨**)。 有效值為：  
  
-   **否**  
  
-   **是**  
  
-   變音符號的相關資訊，請參閱[變音符號](http://go.microsoft.com/fwlink/?LinkId=154091)中 MSN Encarta Encyclopedia 上。  
  
 **上次母體擴展日期**  
 顯示目錄上次擴展的日期。  
  
 **[擁有者]**  
 全文檢索目錄的擁有者。  
  
 **唯一索引鍵計數**  
 構成目錄的全文檢索索引之唯一字的數目。  
  
### <a name="catalog-action"></a>目錄動作  
  
|||  
|-|-|  
|**無**|不會執行 **最佳化目錄**、 **重建目錄**，或 **重新擴展目錄** 等作業。|  
|**最佳化目錄**|最佳化目錄的空間利用，並改善查詢的效能。 它還會改善搜尋結果之次序相關性的精確性。<br /><br /> 此動作會執行 ALTER FULLTEXT CATALOG *catalog_name* REORGANIZE。|  
|**重建目錄**|刪除並重建全文檢索目錄。 如果已變更基礎的目錄屬性 (例如區分腔調字)，就必須執行此項作業。<br /><br /> 為了使重建能順利完成，全文檢索目錄所存在的檔案群組必須在線上，或者可供讀寫。 重建之後，就會重新擴展全文檢索的索引。<br /><br /> 此動作會執行 ALTER FULLTEXT CATALOG *catalog_name* REBUILD。|  
|**重新擴展目錄**|用資料最近的變更來更新目錄。 此選項不需要關閉目錄。|  
  
## <a name="see-also"></a>另請參閱  
 [擴展全文檢索索引](../relational-databases/indexes/indexes.md)  
  
  