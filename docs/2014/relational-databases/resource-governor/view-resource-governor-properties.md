---
title: 檢視資源管理員屬性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35d4720a8fe8b8c1b404a97e27b36896f36dd5f7
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100793"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 [資源管理員屬性] 頁面來建立或設定資源管理員實體，例如資源集區和工作負載群組。  
  
1.  **開始之前：**[Permissions](#Permissions)  
  
2.  **若要檢視資源管理員屬性，請使用：**[資源管理員屬性頁面](#ViewRGProp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 除了檢視資源管理員實體的屬性之外，還可以使用 **[資源管理員屬性]** 頁面執行多個組態工作。 如需詳細資訊，請參閱下列主題：  
  
-   [啟用資源管理員](enable-resource-governor.md)  
  
-   [停用資源管理員](disable-resource-governor.md)  
  
-   [建立資源集區](create-a-resource-pool.md)  
  
-   [建立工作負載群組](create-a-workload-group.md)  
  
-   [變更資源集區設定](change-resource-pool-settings.md)  
  
-   [變更工作負載群組設定](change-workload-group-settings.md)  
  
-   [移動工作負載群組](move-a-workload-group.md)  
  
 加入、刪除或移動工作負載群組或資源集區之後，當您按一下 **[確定]** 時，系統就會執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。  
  
 如果建立或重新設定資源集區或工作負載群組的工作失敗，在屬性頁的標題下方會出現摘要錯誤訊息。 若要查看詳細錯誤訊息，按一下錯誤訊息上的向下箭頭。  
  
 您可以利用查詢 [sys.dm_resource_governor_configuration](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql) 動態管理檢視的方式，查看目前 is_configuration_pending 的狀況，了解是否有暫止的組態。  
  
###  <a name="Permissions"></a> 權限  
 檢視資源管理員屬性需要 VIEW SERVER STATER 權限。 資源管理員組態工作需要 CONTROL SERVER 權限。  
  
##  <a name="ViewRGProp"></a> 檢視 Resource Governor 屬性頁面  
 **若要使用下列項目中的 [Resource Governor 屬性] 頁面來檢視 Resource Governor 屬性： [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，然後遞迴地向下展開 **[管理]** 節點至 **[資源管理員]**。  
  
2.  以滑鼠右鍵按一下 [Resource Governor]，然後按一下 [屬性]，這會開啟 [Resource Governor 屬性] 頁面。  
  
3.  如需有關該頁中之欄位的說明，請參閱＜ [資源管理員屬性](#RGProp)＞。  
  
4.  若要儲存任何變更，請按一下 **[確定]**。  
  
##  <a name="RGProp"></a> 資源管理員屬性  
 **分類函數名稱**  
 從清單中選取以指定分類函數。  
  
 **啟用資源管理員**  
 以選取或清除核取方塊的方式，啟用或停用資源管理員。  
  
 **資源集區**  
 使用提供的方格，建立或變更資源集區組態。 此方格會填入預先定義的內部與預設集區的資訊。 以按一下集區資料列的第一個資料行的方式，選取要進行作業的集區。 若要建立新的資源集區，按一下 資料列加上了星號 (**&#42;**)。  
  
 **名稱**  
 指定資源集區的名稱。  
  
 **最小 CPU %**  
 當 CPU 出現瓶頸時，為在資源集區中的所有要求，指定保證平均 CPU 頻寬使用量。 範圍是 0 到 100。  
  
 **最大 CPU %**  
 當發生 CPU 競爭時，指定所有要求在此資源集區中將會接收的最大平均 CPU 頻寬。 範圍是 0 到 100。 預設設定為 100。  
  
 **最小記憶體 %**  
 指定為此資源集區所保留的最小記憶體數量 (不與其他資源集區共享)。 範圍是 0 到 100。  
  
 **最大記憶體 %**  
 指定在此資源集區中，可供要求所用的伺服器記憶體總量。 範圍是 0 到 100。 預設設定為 100。  
  
 如需詳細資訊，請參閱 <<c0> [ 建立資源集區&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)。</c0>  
  
 **資源集區的工作負載群組**  
 使用提供的方格，建立或變更工作負載群組的組態。 此方格會填入預先定義的內部與預設群組的資訊。 按一下集區資料列的第一個資料行，選取要進行作業的群組。 若要建立新的工作負載群組，按一下 資料列加上了星號 (**&#42;**)。  
  
 **名稱**  
 指定工作負載群組的名稱。  
  
 **重要性**  
 指定在工作負載群組中的要求的相對重要性。 可用的設定為「低」、「中」和「高」。  
  
 **最大要求**  
 指定在工作負載群組中可允許執行的最大同時要求數。 必須是 0 或正整數。  
  
 **CPU 時間 (秒)**  
 指定一個要求所能使用的最大 CPU 時間量。 必須是 0 或正整數。 如果為 0，時間是無限制。  
  
 **記憶體授權 %**  
 指定單一要求可由集區中獲取的記憶體最大數量。 範圍是 0 到 100。  
  
 **授與逾時 (秒)**  
 指定在查詢失敗前，一個查詢能夠等待可用資源的最大時間。 必須是 0 或正整數。  
  
 **平行處理原則的程度**  
 為平行要求指定最大平行程度 (DOP)。 範圍是 0 到 64。  
  
 如需詳細資訊，請參閱 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql) (建立可用性群組 (Transact-SQL))。  
  
## <a name="view-resource-governor-properties-by-using-transact-sql"></a>使用 Transact-SQL 檢視資源管理員屬性  
 **使用 Transact-SQL 檢視資源管理員屬性**  
  
1.  若要檢視 Resource Governor 實體的定義，請使用 [Resource Governor 目錄檢視 &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql)。  
  
2.  若要檢視 Resource Governor 實體的目前組態，請使用 [Resource Governor 相關的動態管理檢視 &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [資源管理員](resource-governor.md)   
 [啟用資源管理員](enable-resource-governor.md)   
 [資源管理員資源集區](resource-governor-resource-pool.md)   
 [資源管理員工作負載群組](resource-governor-workload-group.md)   
 [資源管理員分類函數](resource-governor-classifier-function.md)  
  
  
