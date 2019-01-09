---
title: 進階合併式複寫衝突偵測與解決 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7e8f2f9de721f2e314961a6d2c10cf14c99be53
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786100"
---
# <a name="advanced-merge-replication-conflict-detection-and-resolution"></a>Advanced Merge Replication Conflict Detection and Resolution
  發行者與訂閱者連接並進行同步處理時，合併代理程式會偵測是否有任何衝突。 如果偵測到衝突，「合併代理程式」會使用衝突解析程式 (在發行項加入發行集時指定)，決定要接受及傳播至其他站台的資料。  
  
> [!NOTE]  
>  雖然「訂閱者」會與「發行者」同步，但是衝突通常是在不同「訂閱者」端進行更新之間發生，而不是在「訂閱者」端和「發行者」端進行更新時發生。  
  
 衝突偵測與解決的行為取決於下列選項，這些選項會在本主題中說明：  
  
-   您是否指定資料行層級追蹤、資料列層級追蹤或邏輯記錄層級追蹤。  
  
-   您是否指定預設的優先權式解決機制或指定發行項解析程式。 發行項解析程式可以是：  
  
    -   以 Managed 程式碼撰寫的 *商務邏輯處理常式* 。  
  
    -   以 COM 為基礎的 *自訂解析程式*。  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]提供之以 COM 為基礎的解析程式。  
  
     如果使用預設解析機制，則會依據所用的訂閱類型進一步決定行為：用戶端或伺服器。  
  
## <a name="conflict-detection"></a>衝突偵測  
 資料變更是否算是衝突取決於您為發行項所設定的衝突追蹤類型：  
  
-   當您選取資料行層級衝突追蹤時，如果在一個以上的複寫節點對相同資料列中的相同資料行進行變更，則該變更會被視為衝突。  
  
-   當您選取資料列層級追蹤時，如果在一個以上的複寫節點對相同資料列中的任何資料行進行變更，則該變更會被視為衝突 (對應資料列中受影響的資料行不需要相同)。  
  
-   當您選取邏輯記錄層級追蹤時，如果在一個以上的複寫節點對相同邏輯記錄中的任何資料列進行變更，則該變更會被視為衝突 (對應資料列中受影響的資料行不需要相同)。  
  
 如需詳細資訊，請參閱 [偵測和解決邏輯記錄中的衝突](advanced-merge-replication-conflict-resolving-in-logical-record.md)。  
  
 若要指定發行項的衝突追蹤與解決層級，請參閱＜ [指定合併發行項的衝突追蹤與解決層級](../publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)＞。  
  
## <a name="conflict-resolution"></a>衝突解決  
 在偵測到衝突後，「合併代理程式」會啟動選取的衝突解析程式，並使用該解析程式決定衝突成功者。 成功的資料列已套用至「發行者」與「訂閱者」，而失敗的資料列則已寫入衝突資料表。 衝突會在解析程式執行後立即解決，除非您選擇以互動方式解決衝突。  
  
### <a name="resolver-types"></a>解析程式類型  
 在合併式複寫中，衝突解決會在發行項層級發生。 對於由許多發行項所組成的發行集來說，您可以使用各種不同的衝突解析程式來處理不同的發行項，也可以使用相同的解析程式來解決一個發行項、數個發行項，或者組成發行集的所有發行項。  
  
 如果您計劃使用預設的優先權式衝突解析程式，就無需設定發行項的解析程式屬性。 如果您要使用發行項解析程式而非預設的解析程式，則必須在「發行者」上選取可用的解析程式，以設定要使用此解析程式的發行項之解析程式屬性。 需要傳遞至解析程式的任何特定資訊，也可以在解析程式資訊屬性中指定。  
  
 合併式複寫提供四種類型的衝突解析程式：  
  
-   預設的優先權式衝突解析程式  
  
     根據訂閱是客訂閱或主訂閱而定，預設解決機制的行為會有所差異。 您可指派優先權值給使用主訂閱的個別「訂閱者」；對具有最高優先權的節點所做的變更會在任何衝突中優先。 對於客訂閱，第一個寫入「發行者」的變更會在衝突中優先。  
  
     建立訂閱之後，就不能變更訂閱的類型。  
  
-   商務邏輯處理常式  
  
     商務邏輯處理常式架構允許您撰寫在合併同步處理過程中呼叫的 Managed 程式碼組件。 該組件包含商務邏輯，可在同步處理期間回應衝突及一些其他條件。 如需詳細資訊，請參閱[在合併同步處理期間執行商務邏輯](execute-business-logic-during-merge-synchronization.md)。  
  
-   以 COM 為基礎的自訂解析程式  
  
     合併式複寫提供一個 API，用於以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]等語言將解析程式撰寫為 COM 物件。 如需詳細資訊，請參閱 [COM-Based Custom Resolvers](advanced-merge-replication-conflict-com-based-custom-resolvers.md)。  
  
-    [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含多個以 COM 為基礎的解析程式。 如需詳細資訊，請參閱 [以 COM 為基礎的 Microsoft 解析程式](advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
 如需如何選取適當解析程式類型的詳細資訊，請參閱[選擇解析程式](advanced-merge-replication-conflict-choose-a-resolver.md)。  
  
> [!NOTE]  
>  某些發行項解析程式的撰寫僅供處理特定作業的衝突。 例如，某個解析程式可以處理更新，但無法處理插入或刪除。 預設的優先權式衝突解析程式會處理沒有由發行項解析程式所處理的任何衝突。  
  
 若要指定合併訂閱類型與衝突解決優先權，請參閱  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]:[指定合併訂閱類型和衝突解決優先權&#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   複寫[!INCLUDE[tsql](../../../includes/tsql-md.md)]程式設計與 Replication Management Objects (RMO) 程式設計：[建立提取訂閱](../create-a-pull-subscription.md)和[建立發送訂閱](../create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>互動解析程式  
 複寫提供「互動解析程式」使用者介面，可與預設的優先權式衝突解析程式或發行項解析程式一起使用。 透過 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager 執行視需要的同步處理時，「互動解析程式」會在執行階段顯示衝突資料，並讓您選擇如何解決衝突。 如需有關如何啟用互動式解決及啟動「互動解析程式」的詳細資訊，請參閱＜ [互動式衝突解決](advanced-merge-replication-conflict-interactive-resolution.md)＞。  
  
## <a name="viewing-conflicts"></a>檢視衝突  
 檢視衝突最直接的方法是使用「複寫衝突檢視器」，該檢視器可從 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 取得 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 也提供允許查詢衝突資料表的預存程序)。 「衝突檢視器」和「互動解析程式」是類似的工具，不過「互動解析程式」可讓您在同步處理發生時解決衝突，而「衝突解析程式」是設計用來在已解決衝突後檢視衝突。 如果系統資料表中仍有可用的衝突中繼資料 (衝突中繼資料依預設會保留 14 天)，您可以在「衝突檢視器」中覆寫衝突解決結果，不過如果經常需要直接介入，請考慮使用「互動解析程式」。  
  
> [!NOTE]  
>  「衝突檢視器」中不會顯示涉及邏輯記錄的衝突。 若要檢視這些衝突的相關資訊，請使用複寫預存程序。 如需詳細資訊，請參閱[檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../view-conflict-information-for-merge-publications.md)。  
  
 「衝突檢視器」會顯示下列三個系統資料表中的資訊：  
  
-   複寫會為合併發行項中的每個資料表建立衝突資料表，並使用格式為 **MSmerge_conflict_\<發行集名稱>_\<發行項名稱>** 的名稱。  
  
     衝突資料表的結構與其所根據的資料表相同。 其中一個資料表內的資料列含有衝突資料列的失敗版本 (資料列的優先版本位在實際的使用者資料表中)。  
  
-   **MSmerge_conflicts_info** 資料表提供每一個衝突的相關資訊，包括衝突類型。  
  
-   **sysmergearticles** 資料表可識別哪些使用者資料表具有衝突資料表，並提供衝突資料表的相關資訊。  
  
 依預設，會儲存衝突資訊：  
  
-   如果發行集相容性層級為 90RTM 或更高，則是在「發行者」與「訂閱者」端。  
  
-   如果發行集相容性層級低於 80RTM，則是在發行者端。  
  
-   如果「訂閱者」執行 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]，則會儲存在「發行者」端。 衝突資料無法儲存在 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 訂閱者上。  
  
 **若要檢視衝突**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]:[檢視並解決合併式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](../view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計：[檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>另請參閱  
 [同步處理資料](../synchronize-data.md)  
  
  
