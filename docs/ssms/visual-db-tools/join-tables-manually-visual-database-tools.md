---
title: 手動聯結資料表 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- manual joins [SQL Server]
- joins [SQL Server], manual
- joins [SQL Server], creating
ms.assetid: 9c785356-646b-4c87-82d4-25efd6051d9d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 60cade56837f3941e765419d1216fe1efb089a7a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68253918"
---
# <a name="join-tables-manually-visual-database-tools"></a>手動聯結資料表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在新增兩個 (或更多) 資料表至查詢時， [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 會根據通用資料或資料庫中所儲存有關資料表關聯方式的資訊，聯結這些資料表。 如需詳細資料，請參閱[自動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)。 不過，如果 [查詢和檢視設計師] 尚未自動聯結資料表，或者想要在資料表間建立額外的聯結，則可以手動聯結資料表。  
  
可以根據任兩個資料行間的比較來建立聯結，而不只是根據包含相同資訊的資料行。 例如，如果資料庫包含兩個資料表 `titles` 和 `roysched`，則可以比較 `ytd_sales` 資料表的 `titles` 資料行與 `lorange` 資料表的 `hirange` 和 `roysched` 資料行的值。 建立此聯結將可讓您找到年度迄今的版稅支出落於低和高範圍之間的書名。  
  
> [!TIP]  
> 如果聯結條件中的資料行已經建立索引，則聯結會工作得較快。 在某些狀況下，聯結未建立索引的資料行將導致較慢的查詢。  
  
### <a name="to-manually-join-tables-or-table-structured-objects"></a>若要手動聯結資料表或表格化物件  
  
1.  將想要聯結的物件新增至 [圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  將聯結資料行的名稱拖曳至第一個資料表或表格化物件上，然後將它放在第二個資料表或表格化物件的關聯資料行中。 不可讓聯結以 **text**、 **ntext**或**image** 資料行為基礎。  
  
    > [!NOTE]  
    > 聯結資料行必須具有相同的 (或相容的) 資料類型。 例如，如果第一個資料表的聯結資料行為日期，就必須關聯至第二個資料表的日期資料行。 另一方面，如果第一個聯結資料行為整數，則關聯的聯結資料行也必須為整數資料類型，但其大小可有所不同。 [查詢和檢視設計師] 不會檢查用來建立聯結的資料行資料類型，但在執行查詢時，如果資料類型不相容，則資料庫將顯示錯誤訊息。  
  
3.  必要時，請變更聯結運算子。在預設狀況下，此運算子為等號 (=)。 如需詳細資訊，請參閱[修改聯結運算子 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md)。  
  
查詢和檢視表設計工具會將 INNER JOIN 子句新增至 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中的 SQL 陳述式。 您可以將類型變更為外部聯結 (Outer Join)。 如需詳細資訊，請參閱[建立外部聯結 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-outer-joins-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
