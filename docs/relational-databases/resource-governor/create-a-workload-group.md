---
title: 建立工作負載群組 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 60d01508250c68bfb6143f5f53596fe9fefc4973
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720504"
---
# <a name="create-a-workload-group"></a>建立工作負載群組

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]來建立工作負載群組。  
  
-   **開始之前：** [限制事項](#LimitationsRestrictions)、[權限](#Permissions)  
  
-   **若要建立工作負載群組，請使用下列方式：** [SQL Server Management Studio](#CreRPProp)、[Transact-SQL](#CreRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制事項

 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 非對齊式資料分割資料表上之索引建立所耗用的記憶體，與相關的資料分割數目成正比。 如果所需的總記憶體超出工作負載群組設定所設的每個查詢限制 (REQUEST_MAX_MEMORY_GRANT_PERCENT)，這個索引建立動作可能會失敗。 由於預設工作負載群組允許查詢超過每個查詢限制，而且基於 SQL Server 2005 相容性會啟動所需的記憶體下限，因此使用者或許能夠在預設工作負載群組中執行相同的索引建立動作，但前提是預設資源集區有設定足夠的總記憶體來執行這類查詢。  
  
 允許索引建立使用比一開始授與之記憶體更多的記憶體工作空間來改善效能。 資源管理員支援這種特殊的處理，不過，初始授與和任何額外的記憶體授與都受到工作負載群組和資源集區設定的限制。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 權限

 建立工作負載群組需要 CONTROL SERVER 權限。  
  
##  <a name="create-a-workload-group-using-sql-server-management-studio"></a><a name="CreRPProp"></a> 使用 SQL Server Management Studio 建立工作負載群組

 **若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [物件總管] 中，遞迴地向下展開 **[管理]** 節點至包含要修改之工作負載群組的資源集區。  
  
2.  以滑鼠右鍵按一下 [工作負載群組]  資料夾，然後按一下 [新增工作負載群組]  。  
  
3.  在 **[資源集區]** 方格中，確定已反白顯示要新增工作負載群組的資源集區。  
  
4.  **[資源集區的工作負載群組]** 方格中會新增一行，其中包含空白名稱和其他資料行的預設值。  
  
5.  按一下 **[名稱]** 資料格，然後輸入工作負載群組的名稱。  
  
6.  在資料列中按一下或按兩下要變更預設值的任何其他資料格，然後輸入新值。  
  
7.  若要儲存變更，請按一下 **[確定]** 。  

##  <a name="create-a-workload-group-using-transact-sql"></a><a name="CreRPTSQL"></a> 使用 Transact-SQL 建立工作負載群組  
 **若要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  執行 CREATE WORKLOAD GROUP 陳述式，指定要設定的屬性值。  
  
2.  執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;

 下列範例會在 `groupAdhoc` 資源集區中建立一個名為 `poolAdhoc`的工作負載群組。  
  
```sql
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱

 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [啟用資源管理員](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [建立資源集區](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [變更工作負載群組設定](../../relational-databases/resource-governor/change-workload-group-settings.md)   
 [建立和測試分類使用者定義函數](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
  
