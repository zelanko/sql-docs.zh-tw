---
title: "加入資料表對話方塊 (資料庫設計工具) (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c2019c038704b47f050980016c23bc27c213018
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>加入資料表對話方塊 (資料庫設計工具) (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 讓您在 [資料庫設計工具] 中新增資料表。  
  
> [!NOTE]  
> 如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
## <a name="uielement-list"></a>UIElement 清單  
**[重新整理]**  
重新整理資料表清單，以符合資料庫目前的狀態。  
  
**[加入]**  
加入選取的資料表或多個資料表。  
  
> [!NOTE]  
> 若要將好幾個資料表加入至圖表，可以在按一下 [新增] 之前選取所有資料表。 或是，按兩下每一個要加入的資料表，完成時按一下 [關閉]。  
  
**關閉**  
關閉對話方塊，而不再加入其他資料表。  
  
## <a name="see-also"></a>另請參閱  
[將資料表新增至圖表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
