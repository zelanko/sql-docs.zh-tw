---
description: 加入資料表對話方塊 (資料庫設計工具) (Visual Database Tools)
title: 新增資料表對話方塊 (資料庫設計工具)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 53898206b1111119dad7056e420bf7395d326007
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497315"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>加入資料表對話方塊 (資料庫設計工具) (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
讓您在 [資料庫設計工具] 中加入資料表。  
  
> [!NOTE]  
> 如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
## <a name="ui-element-list"></a>UI 元素清單  
**[重新整理]**  
重新整理資料表清單，以符合資料庫目前的狀態。  
  
**加入**  
加入選取的資料表或多個資料表。  
  
> [!NOTE]  
> 若要將好幾個資料表加入至圖表，可以在按一下 [新增]  之前選取所有資料表。 或是，按兩下每一個要加入的資料表，完成時按一下 [關閉]  。  
  
**關閉**  
關閉對話方塊，而不再加入其他資料表。  
  
## <a name="see-also"></a>另請參閱  
[將資料表新增至圖表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
