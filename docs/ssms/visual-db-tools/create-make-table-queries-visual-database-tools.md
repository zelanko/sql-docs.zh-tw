---
title: 建立製成資料表查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 3152bf516975dc88d9b1bf826dc01775d98f4f05
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67682508"
---
# <a name="create-make-table-queries-visual-database-tools"></a>建立製成資料表查詢 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以使用製成資料表查詢 (Make Table Query)，將資料列複製到新的資料表中；這種方法非常適合用來建立要使用的資料子集，或是將資料表的內容從其中一個資料庫複製到另一個資料庫。 製成資料表查詢與插入結果查詢相似，但前者會建立用來複製資料列的新資料表。  
  
建立製成資料表查詢時，請指定：  
  
-   新資料庫資料表 (目的資料表) 的名稱。  
  
-   從中複製資料列的一或多個資料表 (來源資料表)。 您可以從單一資料表或聯結資料表複製資料列。  
  
-   要從中複製內容的來源資料表資料行。  
  
-   排序次序 (若要以特定次序複製資料列)。  
  
-   搜尋條件，用來定義要複製的資料列。  
  
-   [群組依據] 選項 (如果只要複製摘要資訊)。  
  
例如，下列查詢會建立名為 `uk_customers` 的新資料表，並將 `customers` 資料表中的資訊複製到新資料表中：  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
若要順利使用製成資料表查詢：  
  
-   資料庫必須支援 SELECT...INTO 語法。  
  
-   必須擁有在目標資料庫中建立資料表的使用權限。  
  
### <a name="to-create-a-make-table-query"></a>若要建立製成資料表查詢  
  
1.  將一或多個來源資料表加入至 [圖表] 窗格中。  
  
2.  從 [查詢設計工具]  功能表中，指向 [變更類型]  ，然後按一下 [製成資料表]  。  
  
3.  在 [製成資料表]  對話方塊中，輸入目的資料表的名稱。 查詢和檢視設計師並不會檢查名稱是否存在，或您是否具有建立資料表的權限。  
  
    若要在其他資料庫中建立目的資料表，請指定完整的資料表名稱，包括目標資料庫名稱、擁有人 (如有需要) 和資料表的名稱。  
  
4.  指定並將要複製的資料行加入至查詢中。 如需詳細資訊，請參閱 [將資料行新增至查詢 (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)。 只有加入查詢中的資料行才會複製。 若要複製整個資料列，請選擇 [&#42; (所有資料行)]  。  
  
    查詢和檢視表設計工具會將您選擇的資料行新增至 [準則] 窗格的 [資料行]  資料行。  
  
5.  若要以特定次序複製資料列，請指定排序次序。 如需詳細資訊，請參閱 **排序和群組查詢結果**。  
  
6.  輸入搜尋條件以指定要複製的資料列。 如需詳細資訊，請參閱 [指定搜尋準則 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)。  
  
    如果沒有指定搜尋條件，便會將來源資料表的所有資料列複製到目的資料表中。  
  
    > [!NOTE]  
    > 當將要搜尋的資料行加入至 [準則] 窗格時，[查詢和檢視設計師] 也會將它加入至要複製的資料行清單中。 如果想使用某一資料行進行搜尋但不想複製它，請在代表資料表或表格化物件 (Table-Structured Object) 的矩形中，清除資料行名稱旁的核取方塊。  
  
7.  若要複製摘要資訊，請指定 [群組依據] 選項。 如需詳細資訊，請參閱 [摘要查詢結果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)。  
  
執行製成資料表查詢時， [結果窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)不會報告結果。 而是出現訊息指出已經複製了多少資料列。  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[查詢類型 (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
