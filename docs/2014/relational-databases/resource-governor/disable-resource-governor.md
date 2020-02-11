---
title: 停用資源管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, disabling
ms.assetid: 2c2d2db0-34a5-4f50-b783-17693e3ce3f1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 75feaf114355c3a23abad6ec23be9011e0de5e06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63209717"
---
# <a name="disable-resource-governor"></a>停用資源管理員
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 停用資源管理員。  
  
-   **開始之前：** [限制事項](#LimitationsRestrictions)、[權限](#Permissions)  
  
-   **若要停用 Resource Governor，請使用下列方式：** [物件總管](#RGOffObjEx)、[Resource Governor 屬性](#RGOffProp)、[Transact-SQL](#RGOffTSQL)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 停用資源管理員會產生下列結果：  
  
-   系統不會執行分類函數。  
  
-   所有新的連接都會自動分類至預設工作負載群組中。  
  
-   系統起始的要求會分類至內部工作負載群組中。  
  
-   所有現有的工作負載群組和資源集區設定都會重設為預設值。 在此情況下，如果到達限制，系統將不會引發任何事件。  
  
-   一般的系統監視不會受到影響。  
  
-   您可以變更組態，但這些變更在資源管理員啟用之後才會生效。  
  
-   一旦重新啟動 SQL Server 之後，資源管理員將不會載入其組態，而是只有預設和內部工作負載群組與資源集區。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 在使用者交易中時，您無法使用 `ALTER RESOURCE GOVERNOR` 陳述式停用資源管理員。  
  
###  <a name="Permissions"></a> 權限  
 停用資源管理員需要 CONTROL SERVER 權限。  
  
##  <a name="RGOffObjEx"></a> 使用物件總管停用資源管理員  
 **若要使用物件總管停用資源管理員**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 **[管理]** 節點至 **[資源管理員]** 。  
  
2.  以滑鼠右鍵按一下 [資源管理員]  ，然後按一下 [停用]  。  
  
##  <a name="RGOffProp"></a> 使用資源管理員屬性停用資源管理員  
 **若要使用資源管理員屬性頁面來停用資源管理員**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 **[管理]** 節點至 **[資源管理員]** 。  
  
2.  以滑鼠右鍵按一下 [資源管理員]  ，然後按一下 [屬性]  ，這會開啟 [資源管理員屬性]  頁面。  
  
3.  按一下 **[啟用資源管理員]** 核取方塊，確定未選取方塊，然後按一下 **[確定]** 。  
  
##  <a name="RGOffTSQL"></a> 使用 Transact-SQL 停用資源管理員  
 **若要使用 Transact-SQL 停用資源管理員**  
  
1.  執行 **ALTER RESOURCE GOVERNOR DISABLE** 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;  
 下列範例會啟用資源管理員。  
  
```  
ALTER RESOURCE GOVERNOR DISABLE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](resource-governor.md)   
 [啟用資源管理員](enable-resource-governor.md)   
 [資源管理員資源集區](resource-governor-resource-pool.md)   
 [資源管理員工作負載群組](resource-governor-workload-group.md)   
 [資源管理員分類函數](resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
