---
title: 更新資料表對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8c5575f73ff75ef9276bab52571e8670f28e0be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63204676"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>更新資料表對話方塊 (Visual Database Tools)
  這個對話方塊可以讓您指定要更新的資料表。  
  
 當您將查詢類型變更為更新查詢時，如果 [圖表] 窗格中顯示一個以上的資料表，此對話方塊就會出現。  
  
 選取要更新的資料表，然後選擇 [**確定]**。  
  
> [!NOTE]  
>  如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
## <a name="see-also"></a>另請參閱  
 [建立更新查詢 &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
