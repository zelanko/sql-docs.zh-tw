---
title: 移動工作負載群組 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties_moveworkloadgroup.f1
helpviewer_keywords:
- workload groups [SQL Server], move
- Resource Governor, workload group move
ms.assetid: f2068636-6e53-486a-a6fc-c12de2a38424
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8d1eb983f32e995d974ffbfb460e679f715d20ac
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="move-a-workload-group"></a>移動工作負載群組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 將資源管理員工作負載群組移至不同的資源集區。  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **SQL Server Management Studio**  [Transact-SQL](#MoveWGSSMS)、 [來移動工作負載群組](#MoveWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 如果有暫止的資源管理員組態作業，則無法移動工作負載群組。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 如果有暫止的資源管理員組態作業，則無法移動工作負載群組。 您可以藉由查詢 [sys.dm_resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) 動態管理檢視的方式，查看目前 is_configuration_pending 的狀況，以判斷是否有暫止的組態。  
  
###  <a name="Permissions"></a> 權限  
 移動工作負載群組需要 CONTROL SERVER 權限。  
  
##  <a name="MoveWGSSMS"></a> 使用 SQL Server Management Studio 移動工作負載群組  
 **若要使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**  
  
1.  在 [物件總管] 中，遞迴地向下展開 **[管理]** 節點至 **[資源管理員]**。  
  
2.  以滑鼠右鍵按一下 [資源管理員]，然後按一下 [屬性]，這會開啟 [資源管理員屬性] 頁面。  
  
3.  在 **[資源集區]** 視窗中，按一下包含要移動之工作負載群組的資源集區。 **[工作負載群組]** 視窗現在會列出該資源集區中的工作負載群組。  
  
4.  在 [工作負載群組] 視窗中，以滑鼠右鍵按一下要移動之工作負載群組左側的向右箭頭，然後按一下 [移至]。 這會顯示 **[移動工作負載群組]** 視窗。  
  
5.  可用的資源集區會顯示在此視窗中。 按一下您想要將工作負載群組移到其中的資源集區名稱，然後按一下 **[確定]** 執行此動作。  
  
6.  等到您按一下 **[確定]** 之後，這個動作才會完成。 當您按一下 **[確定]**，就會執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。  
  
7.  如果建立或重新設定資源集區或工作負載群組的作業失敗，在屬性頁的標題下方會出現摘要錯誤訊息。 若要查看詳細錯誤訊息，按一下錯誤訊息上的向下箭頭。  
  
##  <a name="MoveWGTSQL"></a> 使用 Transact-SQL 移動工作負載群組  
 **若要使用 Transact-SQL 移動工作負載群組**  
  
1.  執行 **ALTER WORKLOAD GROUP** 陳述式，並指定要移動之工作負載群組的名稱以及要移入的資源集區。  
  
2.  執行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 陳述式。  
  
### <a name="example-transact-sql"></a>範例 &#40;Transact-SQL&#41;  
 下列範例會將名為 `groupAdhoc` 的工作負載群組移至預設資源集區。  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [[資源管理員]](../../relational-databases/resource-governor/resource-governor.md)   
 [啟用資源管理員](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [建立資源集區](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [建立工作負載群組](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
