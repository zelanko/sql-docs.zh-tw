---
title: 刪除工作負載群組 | Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], delete
- Resource Governor, workload group delete
ms.assetid: d5902c46-5c28-4ac1-8b56-cb4ca2b072d0
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b4b322231f546871d5581de470fdc894ed4fe41e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68099264"
---
# <a name="delete-a-workload-group"></a>刪除工作負載群組
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 刪除工作負載群組或資源集區。  
  
-   **開始之前：** [限制事項](#LimitationsRestrictions)、[權限](#Permissions)  
  
-   **若要刪除工作負載群組，請使用下列方式：** [物件總管](#DelWGObjEx)、[Resource Governor 屬性](#DelWGRGProp)、[Transact-SQL](#DelWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 如果工作負載群組包含作用中工作階段，您就無法刪除該工作負載群組。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 如果工作負載群組包含使用中工作階段，當呼叫 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式以套用變更時，刪除工作負載群組或將工作負載群組移到不同的資源集區將會失敗。 若要避免這個問題，您可以採取下列其中一個動作：  
  
-   等到受影響之群組的所有工作階段已經中斷連接後，重新執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。  
  
-   在受影響的群組中，使用 KILL 命令明確地停止工作階段，然後重新執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。 在您使用 [刪除]  之後但停止使用中工作階段之前，如果您決定不想要明確地停止工作階段，請使用原始名稱來重新建立群組，然後將該群組移到原始的資源集區。  
  
-   重新啟動伺服器。 重新啟動程序完成後，將不會建立已經刪除的群組，而且已經移動的群組將會使用新的資源集區指派。  
  
###  <a name="Permissions"></a> 權限  
 刪除工作負載群組需要 CONTROL SERVER 權限。  
  
##  <a name="DelWGObjEx"></a> 使用物件總管刪除工作負載群組  
 **若要使用物件總管刪除工作負載群組**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 **[管理]** 節點至 **[資源集區]** 。  
  
2.  遞迴地向下展開 **[資源集區]** 至資源集區中的 **[工作負載群組]** 節點，此資源集區包含要刪除的工作負載群組。  
  
3.  以滑鼠右鍵按一下工作負載群組，然後按一下 [刪除]  。  
  
4.  在 **[刪除物件]** 視窗中，工作負載群組便列於 **[要刪除的物件]** 清單內。 若要刪除工作負載群組，請按一下 **[確定]** 。  
  
##  <a name="DelWGRGProp"></a> 使用資源管理員屬性刪除工作負載群組  
 **若要使用資源管理員屬性頁面來刪除工作負載群組**  
  
1.  在 [物件總管] 中，遞迴地展開 **[管理]** 節點底下，包括 **[資源集區]** 。  
  
2.  以滑鼠右鍵按一下包含要修改之工作負載群組的資源集區，然後選取 [屬性]  。 這會開啟 **[資源管理員屬性]** 頁面。  
  
3.  在 [資源集區的工作負載群組]  視窗中，按一下要刪除之工作負載群組的資料列，然後以滑鼠右鍵按一下資料列左側的向右箭頭，再按一下 [刪除]  。  
  
4.  若要刪除工作負載群組，請按一下 **[確定]** 。  
  
##  <a name="DelWGTSQL"></a> 使用 Transact-SQL 刪除工作負載群組  
 **若要使用 Transact-SQL 刪除工作負載群組**  
  
1.  執行 **DROP WORKLOAD GROUP** 陳述式，並指定要刪除之工作負載群組的名稱。  
  
2.  在您發出 **ALTER RESOURCE GOVERNOR RECONFIGURE** 陳述式之前，請先確認要刪除的工作負載群組中沒有任何使用中要求。 如果存在使用中要求， **ALTER RESOURCE GOVERNOR** 將會失敗。 若要避免這個問題，您可以採取下列其中一個動作：  
  
    -   等候直到工作負載群組的所有工作階段都中斷連接為止。  
  
    -   使用 **KILL** 命令來明確地停止工作負載群組中的工作階段。  
  
    -   重新啟動伺服器。 系統不會重新建立工作負載群組。  
  
    -   在您已經發出 **DROP WORKLOAD GROUP** 陳述式但決定您不要明確地停止工作階段以套用變更的實例中，您可以使用您發出 DROP 陳述式前的相同名稱重新建立群組，然後將該群組移到原始的資源集區。  
  
3.  執行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;  
 下列範例會卸除名稱為 `groupAdhoc`的工作負載群組。  
  
```  
DROP WORKLOAD GROUP groupAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [建立資源集區](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [建立工作負載群組](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [刪除資源集區](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
