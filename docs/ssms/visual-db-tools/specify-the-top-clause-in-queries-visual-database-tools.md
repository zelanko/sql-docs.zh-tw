---
title: 在查詢中指定 TOP 子句
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- TOP clause, queries
- percentage of rows returned [SQL Server]
- number of rows
- search conditions [SQL Server], TOP clause
- restricting rows returned
- search criteria [SQL Server], limiting rows returned
- inspecting portion of results
- limiting rows returned
- search criteria [SQL Server], TOP clause
ms.assetid: ba7d7c10-9bb3-4d9b-90b0-5fa94ecae59b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 7995bd9ac78595200f6ded5e23c0f0b40cf3ff66
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254926"
---
# <a name="specify-the-top-clause-in-queries-visual-database-tools"></a>在查詢中指定 TOP 子句 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
TOP 子句只傳回查詢中的前 *n* 或百分之 *n* 個資料列。 當您要調查結果的一部份，以了解查詢是否如預期運作時，TOP 子句會很有用，它不會使用傳回全部查詢結果所需的資源。  
  
### <a name="to-specify-the-top-clause-in-queries"></a>若要指定查詢中的 TOP 子句  
  
1.  在 [方案總管] 中開啟查詢或建立新查詢。  
  
2.  從 [檢視]  功能表中，按一下 [屬性視窗]  。  
  
3.  在 [屬性視窗]  中，找出並展開 [Top 規格]  屬性。  
  
4.  按一下 [(Top)]  子屬性，並將其設定為 [Yes]  。  
  
5.  在 [Expression]  子屬性中，輸入有數字結果 (例如 10 或 2*5) 的運算式。  
  
6.  按一下 [Percent]  子屬性，並指示是否將 [Expression]  屬性視為所有傳回資料列的百分比 (Yes)，或視為傳回資料列的絕對值 (No)。  
  
7.  如果查詢使用 ORDER BY 子句，請按一下 [With Ties]  子屬性，並選擇 [Yes]  以顯示群組中的所有資料列 (如果此群組有一部份包含在內)，或選擇 [No]  將它們截斷。  
  
在進行先前的程序之後，注意 SQL 窗格中顯示的 TOP 子句會變更，以反映目前的屬性設定。  
  
> [!NOTE]  
> 您也可以編輯 SQL 窗格中的 TOP 子句，以變更 [Top 規格]  中的子屬性值。  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[查詢屬性 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-properties-visual-database-tools.md)  
  
