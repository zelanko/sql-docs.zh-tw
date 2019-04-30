---
title: 刪除資源集區 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool delete
- resource pools [SQL Server], delete
ms.assetid: 3bdd348b-6582-4ffa-80ef-d49e50596ce5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6e2e9582e8a279be37e05e9ee13a858abb431987
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205841"
---
# <a name="delete-a-resource-pool"></a>刪除資源集區
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 刪除資源集區。  
  
-   **開始之前：**[限制事項](#LimitationsRestrictions)、[權限](#Permissions)  
  
-   **若要刪除資源集區，請使用下列方式：**[SQL Server Management Studio](#DelRPSSMS)、[Transact-SQL](#DelRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 如果資源集區包含工作負載群組，您就無法刪除該資源集區。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 您無法刪除資源管理員的預設或內部資源集區。 如果資源集區包含工作負載群組，您就無法刪除該資源集區。 如需詳細資訊，請參閱 [Delete a Workload Group](delete-a-workload-group.md)。  
  
###  <a name="Permissions"></a> 權限  
 刪除資源集區需要 CONTROL SERVER 權限。  
  
##  <a name="DelRPSSMS"></a> 使用物件總管刪除資源集區  
 **若要使用 SQL Server Management Studio 刪除資源集區**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 **[管理]** 節點至 **[資源管理員]**。  
  
2.  以滑鼠右鍵按一下要刪除的資源集區，然後按一下 [刪除]。  
  
3.  在 **[刪除物件]** 視窗中，資源集區列於 **[要刪除的物件]** 清單內。 若要刪除資源集區，請按一下 **[確定]**。  
  
    > [!NOTE]  
    >  如果您嘗試刪除的資源集區包含工作負載群組，這項動作將會失敗。  
  
##  <a name="DelRPTSQL"></a> 使用 Transact-SQL 刪除資源集區  
 **若要使用 Transact-SQL 刪除資源集區**  
  
1.  執行 `DROP RESOURCE POOL` 陳述式，並指定要刪除之資源集區的名稱。  
  
2.  執行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;  
 下列範例會卸除名稱為 `poolAdhoc`的工作負載群組。  
  
```  
DROP RESOURCE POOL poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](resource-governor.md)   
 [Resource Governor 資源集區](resource-governor-resource-pool.md)   
 [建立資源集區](create-a-resource-pool.md)   
 [變更資源集區設定](change-resource-pool-settings.md)   
 [資源管理員工作負載群組](resource-governor-workload-group.md)   
 [資源管理員分類函數](resource-governor-classifier-function.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-workload-group-transact-sql)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
