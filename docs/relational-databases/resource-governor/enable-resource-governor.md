---
title: 啟用資源管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, enabling
ms.assetid: 4d17af53-cf11-4ce4-aab4-deda94a49836
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 23ff55d4fcb9e9cf398e732376a01ab5495b2a4b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68099254"
---
# <a name="enable-resource-governor"></a>啟用資源管理員
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  預設會關閉資源管理員。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 啟用資源管理員。  
  
-   **開始之前：** [限制事項](#LimitationsRestrictions)、[權限](#Permissions)  
  
-   **若要啟用 Resource Governor，請使用下列方式：** [物件總管](#RGOnObjEx)、[Resource Governor 屬性](#RGOnProp)、[Transact-SQL](#RGOnTSQL)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 啟用資源管理員會產生下列結果：  
  
-   系統會針對新的連接執行分類函數，以便將其工作負載指派給工作負載群組。  
  
-   系統會接受並強制執行資源管理員組態中指定的資源限制。  
  
-   啟用資源管理員之前存在的要求會受到停用資源管理員時所做的任何組態變更影響。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 在使用者交易中時，您無法使用 **ALTER RESOURCE GOVERNOR** 陳述式啟用資源管理員。  
  
###  <a name="Permissions"></a> 權限  
 啟用資源管理員需要 CONTROL SERVER 權限。  
  
##  <a name="RGOnObjEx"></a> 使用物件總管啟用資源管理員  
 **若要使用物件總管啟用資源管理員**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 **[管理]** 節點至 **[資源管理員]** 。  
  
2.  以滑鼠右鍵按一下 [資源管理員]  ，然後按一下 [啟用]  。  
  
##  <a name="RGOnProp"></a> 使用資源管理員屬性啟用資源管理員  
 **若要使用資源管理員屬性頁面來啟用資源管理員**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 **[管理]** 節點至 **[資源管理員]** 。  
  
2.  以滑鼠右鍵按一下 [資源管理員]  ，然後按一下 [屬性]  ，這會開啟 [資源管理員屬性]  頁面。  
  
3.  按一下 **[啟用資源管理員]** 核取方塊，然後按一下 **[確定]** 。  
  
##  <a name="RGOnTSQL"></a> 使用 Transact-SQL 啟用資源管理員  
 **若要使用 Transact-SQL 啟用資源管理員**  
  
1.  執行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;  
 下列範例會啟用資源管理員。  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [停用資源管理員](../../relational-databases/resource-governor/disable-resource-governor.md)   
 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [資源管理員工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [資源管理員分類函數](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
