---
title: 建立全文檢索搜尋查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: de064177558169db099f73e1b4ae113a9f7d2569
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65099448"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>建立全文檢索搜尋查詢 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
全文檢索搜尋會使用 CONTAINS 述詞 (Predicate)，找出在指定資料行中具有指定文字的資料列。 全文檢索搜尋只適用於具有現用全文檢索索引的資料行。 如果您嘗試在未具有目前現用全文檢索索引的資料行上使用 CONTAINS 子句，您會收到錯誤訊息。 如需全文檢索索引和 CONTAINS 子句的詳細資訊，請參閱 [全文檢索搜尋 (SQL Server)](../../relational-databases/search/full-text-search.md) 和 [CONTAINS (Transact-SQL)](https://msdn.microsoft.com/996c72fc-b1ab-4c96-bd12-946be9c18f84)。  
  
### <a name="to-create-a-full-text-search-query"></a>建立全文檢索搜尋查詢  
  
1.  在 [方案總管] 中開啟查詢或建立新查詢。  
  
2.  在查詢的 WHERE 子句中，使用 CONTAINS 函數來搜尋全文檢索資料行。  
  
## <a name="see-also"></a>另請參閱  
[支援的查詢類型 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[使用查詢執行基本作業 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
