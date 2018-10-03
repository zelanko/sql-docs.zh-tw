---
title: 變更資源集區設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9c81b1c82932fe09a89ffb32f17fd32de34ad8d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183018"
---
# <a name="change-resource-pool-settings"></a>變更資源集區設定
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]來變更資源集區設定。  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **使用下列項目變更資源集區的設定**  [SQL Server Management Studio](#ChgRPProp)、 [Transact-SQL](#ChgRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 最大 CPU 百分比必須大於或等於最小 CPU 百分比。 最大記憶體百分比必須大於或等於最小記憶體百分比。  
  
 所有資源集區之最小 CPU 百分比和最小記憶體百分比的總和不得超過 100。  
  
###  <a name="Permissions"></a> 權限  
 變更資源集區設定需要 CONTROL SERVER 權限。  
  
##  <a name="ChgRPProp"></a> 使用 SQL Server Management Studio 變更資源集區設定  
 **若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 [管理]  節點至 [資源集區] 。  
  
2.  以滑鼠右鍵按一下要修改的資源集區，然後按一下 [屬性]。  
  
3.  在 **[資源管理員屬性]** 頁面的 **[資源集區]** 方格中，選取資源集區的資料列 (如果系統沒有自動選取的話)。  
  
4.  在資料列中按一下或按兩下要變更的資料格，然後輸入新值。  
  
5.  若要儲存變更，請按一下 **[確定]**。  
  
##  <a name="ChgRPTSQL"></a> 使用 Transact-SQL 變更資源集區設定  
 **若要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  執行 `ALTER RESOURCE POOL` 陳述式，並指定要變更的屬性值。  
  
2.  執行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;  
 下列範例會變更名為 `poolAdhoc`的資源集區的最大 CPU 百分比設定。  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](resource-governor.md)   
 [啟用資源管理員](enable-resource-governor.md)   
 [建立資源集區](create-a-resource-pool.md)   
 [刪除資源集區](delete-a-resource-pool.md)   
 [資源管理員工作負載群組](resource-governor-workload-group.md)   
 [資源管理員分類函數](resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
