---
title: 更新資料表對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9482391137fa5a1f12fa12defcfde274c0bac680
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33048645"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>更新資料表對話方塊 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
這個對話方塊可以讓您指定要更新的資料表。  
  
當您將查詢類型變更為更新查詢時，如果 [圖表] 窗格中顯示一個以上的資料表，此對話方塊就會出現。  
  
選取要更新的資料表，然後選擇 [確定]。  
  
> [!NOTE]  
> 如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
## <a name="see-also"></a>另請參閱  
[建立更新查詢 (Visual Database Tools)](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)  
  
