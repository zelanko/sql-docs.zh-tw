---
title: 使用容錯移轉可用性群組精靈 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.failoverwizard.progress.f1
- sql12.swb.failoverwizard.f1
- sql12.swb.failoverwizard.selectnewprimary.f1
- sql12.swb.failoverwizard.confirmdataloss.f1
- sql12.swb.failoverwizard.connecttoreplicas.f1
helpviewer_keywords:
- failover [SQL Server], failover
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], configuring
ms.assetid: 4a602584-63e4-4322-aafc-5d715b82b834
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62fb2107b74518afbf55b64057aec63c4e2eec36
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206218"
---
# <a name="use-the-fail-over-availability-group-wizard-sql-server-management-studio"></a>使用容錯移轉可用性群組精靈 (SQL Server Management Studio)
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 PowerShell，針對 AlwaysOn 可用性群組執行規劃的手動容錯移轉或強制手動容錯移轉 (強制容錯移轉)。 可用性群組會在可用性複本層級容錯移轉。 如果您容錯移轉至處於 SYNCHRONIZED 狀態的次要複本，此精靈就會執行規劃的手動容錯移轉 (不會遺失資料)。 如果您容錯移轉至處於 UNSYNCHRONIZED 或 NOT SYNCHRONIZING 狀態的次要複本，此精靈就會執行強制手動容錯移轉，也稱為「強制容錯移轉」  (可能會遺失資料)。 這兩種手動容錯移轉形式都會將您所連接的次要複本轉換成主要角色。 規劃的手動容錯移轉目前會將先前的主要複本會轉換成次要角色。 強制容錯移轉之後，當先前的主要複本上線時，它就會轉換成次要角色。  
  


  
-   **[!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)] 頁面：**  
  
     [選取新的主要複本頁面](#SelectNewPrimaryReplica) (本主題稍後)  
  
     [連接到複本頁面](#ConnectToReplica) (本主題稍後)  
  
     [確認可能遺失資料頁面](#ConfirmPotentialDataLoss) (本主題稍後)  
  
     [摘要頁面&#40;AlwaysOn 可用性群組精靈&#41;](summary-page-always-on-availability-group-wizards.md)  
  
     [進度頁面&#40;AlwaysOn 可用性群組精靈&#41;](progress-page-always-on-availability-group-wizards.md)  
  
     [結果頁面&#40;AlwaysOn 可用性群組精靈&#41;](results-page-always-on-availability-group-wizards.md)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 第一次進行規劃的手動容錯移轉之前，請參閱 [執行可用性群組的已規劃手動容錯移轉 &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)或 PowerShell，針對 AlwaysOn 可用性群組執行規劃的手動容錯移轉或強制手動容錯移轉 (強制容錯移轉)。  
  
 第一次進行強制容錯移轉之前，請先參閱 [執行可用性群組的強制手動容錯移轉 &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)或 PowerShell，針對 AlwaysOn 可用性群組執行規劃的手動容錯移轉或強制手動容錯移轉 (強制容錯移轉)。  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   目標次要複本接受命令之後，容錯移轉命令就會傳回。 不過，在可用性群組完成容錯移轉之後，會以非同步方式復原資料庫。  
  
-   容錯移轉時，不會保留可用性群組內跨資料庫的一致性。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 不支援跨資料庫交易和分散式交易。 如需詳細資訊，請參閱[資料庫鏡像或 AlwaysOn 可用性群組不支援跨資料庫交易 &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md)。  
  
###  <a name="Prerequisites"></a> 使用容錯移轉可用性群組精靈的必要條件  
  
-   您必須連接到裝載目前可用之可用性複本的伺服器執行個體。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要使用容錯移轉可用性群組精靈**  
  
1.  在 [物件總管] 中，連接到裝載需要容錯移轉之可用性群組次要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  若要啟動 [容錯移轉可用性群組精靈]，請以滑鼠右鍵按一下您要容錯移轉的可用性群組，然後選取 [容錯移轉]。  
  
4.  **[簡介]** 頁面所呈現的資訊主要取決於任何次要複本是否符合規劃容錯移轉的資格。 如果此頁面顯示 **[執行這個可用性群組的計劃的容錯移轉]**，表示您可以在不遺失資料的情況下容錯移轉可用性群組。  
  
5.  在 [選取新的主要複本]  頁面上，您可以在選擇將成為新主要複本的次要複本 (「容錯移轉目標」 ) 之前，檢視目前主要複本和 WSFC 仲裁的狀態。 若為規劃的手動容錯移轉，請務必選取 **[容錯移轉整備]** 值為 **[無資料遺失]** 的次要複本。 若為強制容錯移轉，則對於所有可能的容錯移轉目標而言，這個值都是「**資料遺失，警告(***#***)**」，其中 *#* 表示指定次要複本所存在的警告數目。 若要檢視給定容錯移轉目標的警告，請按一下其 [容錯移轉整備] 值。  
  
     如需詳細資訊，請參閱本主題稍後的＜ [選取新的主要複本頁面](#SelectNewPrimaryReplica)＞。  
  
6.  在 **[連接到複本]** 頁面上，連接到容錯移轉目標。 如需詳細資訊，請參閱本主題稍後的＜ [連接到複本頁面](#ConnectToReplica)＞。  
  
7.  如果您正在執行強制容錯移轉，此精靈會顯示 **[確認可能遺失資料]** 頁面。 若要繼續進行容錯移轉，您必須選取 **[按一下這裡確認可能遺失資料的容錯移轉]**。 如需詳細資訊，請參閱本主題稍後的＜[確認可能遺失資料頁面](#ConfirmPotentialDataLoss)＞。  
  
8.  在 **[摘要]** 頁面上，檢閱容錯移轉至選取次要複本的影響。  
  
     如果您對所做的選擇感到滿意時，可以選擇按一下 **[指令碼]** ，建立精靈將執行之步驟的指令碼。 然後，若要將可用性群組容錯移轉至選取的次要複本，請按一下 **[完成]**。  
  
9. **[進度]** 頁面會顯示容錯移轉可用性群組的進度。  
  
10. 當容錯移轉作業完成時， **[結果]** 頁面就會顯示結果。 當精靈完成時，按一下 **[關閉]** 以結束。  
  
     如需詳細資訊，請參閱[結果頁面 &#40;AlwaysOn 可用性群組精靈&#41;](results-page-always-on-availability-group-wizards.md)。  
  
11. 強制容錯移轉之後，請參閱[執行可用性群組的強制手動容錯移轉 &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) 中的＜後續操作：強制容錯移轉之後＞一節。  
  
## <a name="help-for-pages-that-are-exclusive-to-this-wizard"></a>此精靈專用頁面的說明  
 本節描述的是 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]特有的頁面。  
  
 
  
 此精靈的其他頁面都與一個或多個其他 AlwaysOn 可用性群組精靈共用說明，而且記載於個別的 F1 說明主題中。  
  
###  <a name="SelectNewPrimaryReplica"></a> Select New Primary Replica Page  
 本節描述的是 **[選取新的主要複本]** 頁面的選項。 您可以使用此頁面來選取可用性群組將容錯移轉的目標次要複本 (容錯移轉目標)。 這個複本將成為新的主要複本。  
  
#### <a name="page-options"></a>頁面選項  
 **目前的主要複本**  
 顯示目前主要複本的名稱 (如果它已上線的話)。  
  
 **主要複本狀態**  
 顯示目前主要複本的狀態 (如果它已上線的話)。  
  
 **仲裁狀態**  
 顯示可用性複本的 WSFC 仲裁狀態，它有下列幾種：  
  
|值|描述|  
|-----------|-----------------|  
|**一般仲裁**|叢集已經使用一般仲裁來啟動。|  
|**強制仲裁**|叢集已經使用強制仲裁來啟動。|  
|**未知的仲裁**|無法取得叢集仲裁狀態。|  
|**不適用**|裝載可用性複本的節點沒有任何仲裁。|  
  
 如需詳細資訊，請參閱 [WSFC 仲裁模式和投票組態 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)。  
  
 **選擇新的主要複本**  
 您可以使用此方格來選取要成為新主要複本的次要複本。 此方格中的資料行如下所示：  
  
 **伺服器執行個體**  
 顯示裝載次要複本之伺服器執行個體的名稱。  
  
 **可用性模式**  
 顯示伺服器執行個體的可用性模式，它有下列幾種：  
  
|值|描述|  
|-----------|-----------------|  
|**同步認可**|在同步認可模式下認可交易之前，同步認可主要複本會等候同步認可次要複本確認它已完成強行寫入記錄。 同步認可模式可確定，一旦給定次要資料庫與主要資料庫同步處理之後，認可的交易就會受到完整保護。|  
|**非同步認可**|在非同步認可模式下，主要複本會認可交易，而不等候確認非同步認可次要複本已經強行寫入記錄。 非同步認可模式會將次要資料庫上的交易延遲降至最低，但允許這些資料庫落後主要資料庫，因此可能會發生資料遺失。|  
  
 如需詳細資訊，請參閱 <<c0> [ 可用性模式 （AlwaysOn 可用性群組）](availability-modes-always-on-availability-groups.md)。  
  
 **容錯移轉模式**  
 顯示伺服器執行個體的容錯移轉模式，它有下列幾種：  
  
|值|描述|  
|-----------|-----------------|  
|**Automatic**|每當次要複本與主要複本同步處理時，設定為自動容錯移轉的次要複本也支援規劃的手動容錯移轉。|  
|**Manual**|手動容錯移轉的類型有兩種：規劃 (不會遺失資料) 和強制 (可能會遺失資料)。 給定的次要複本會根據次要複本的可用性模式和同步處理狀態 (同步認可模式)，僅支援其中一種類型。 若要判斷給定次要複本目前支援的手動容錯移轉形式，請查看此方格的 **[容錯移轉整備]** 資料行。|  
  
 如需詳細資訊，請參閱[容錯移轉及容錯移轉模式 &#40;AlwaysOn 可用性群組&#41;](failover-and-failover-modes-always-on-availability-groups.md)。  
  
 **[容錯移轉整備]**  
 顯示次要複本的容錯移轉整備，它有下列幾種：  
  
|值|描述|  
|-----------|-----------------|  
|**[無資料遺失]**|這個次要複本目前支援規劃的容錯移轉。 只有當同步認可模式的次要複本目前與主要複本同步處理時，才會出現此值。|  
|**資料遺失，警告(** *#* **)**|這個次要複本目前支援強制容錯移轉 (可能會遺失資料)。 每當次要複本並未與主要複本同步處理時，就會出現此值。 如需有關可能遺失資料的詳細資訊，請按一下資料遺失警告連結。|  
  
 **重新整理**  
 按一下可更新方格。  
  
 **取消**  
 按一下可取消精靈。 在 **[選取新的主要複本]** 頁面上，取消精靈會導致精靈結束，而不執行任何動作。  
  
###  <a name="ConfirmPotentialDataLoss"></a> Confirm Potential Data Loss Page  
 本節描述的是 **[確認可能遺失資料]** 頁面的選項 (只有當您正在執行強制容錯移轉時，才會顯示此頁面)。 本主題僅供 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]使用。 您可以使用此頁面來指出是否願意承擔可能遺失資料的風險，以便強制可用性群組容錯移轉。  
  
#### <a name="confirm-potential-data-loss-options"></a>確認可能遺失資料選項  
 如果選取的次要複本並未與主要複本同步處理，此精靈就會顯示一則警告，表示容錯移轉至此次要複本可能會導致一個或多個資料庫的資料遺失。  
  
 **按一下這裡確認可能遺失資料的容錯移轉**  
 如果您願意承擔遺失資料的風險，以便將這個可用性群組中的資料庫提供給使用者，請按一下此核取方塊。 如果您不願意承擔遺失資料的風險，可以按一下 **[上一步]** 返回 **[選取新的主要複本]** 頁面，或按一下 **[取消]** 結束精靈而不容錯移轉可用性群組。  
  
 **取消**  
 按一下可取消精靈。 在 **[確認可能遺失資料]** 頁面上，取消精靈會導致精靈結束，而不執行任何動作。  
  
###  <a name="ConnectToReplica"></a> Connect to Replica Page  
 本節描述的是 **之** [連接到複本] [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]頁面的選項。 只有當您沒有連接到目標次要複本時，才會顯示此頁面。 您可以使用此頁面來連接到已選取成為新主要複本的次要複本。  
  
#### <a name="page-options"></a>頁面選項  
 **方格資料行：**  
 **伺服器執行個體**  
 顯示將裝載可用性複本的伺服器執行個體名稱。  
  
 **連線方式**  
 顯示在建立連接後連接到伺服器執行個體的帳戶。 如果此資料行對於給定的伺服器執行個體顯示 **[未連接]**，您就必須按一下 **[連接]** 按鈕。  
  
 **[連接]**  
 如果這個伺服器執行個體是在與其他需要連接的伺服器執行個體不同的帳戶下執行，請按一下此按鈕。  
  
 **取消**  
 按一下可取消精靈。 在 **[連接到複本]** 頁面上，取消精靈會導致精靈結束，而不執行任何動作。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [ 可用性模式 （AlwaysOn 可用性群組）](availability-modes-always-on-availability-groups.md)   
 [容錯移轉及容錯移轉模式&#40;AlwaysOn 可用性群組&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [執行可用性群組的已規劃手動容錯移轉 &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)   
 [執行可用性群組的強制手動容錯移轉 &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)   
 [透過強制仲裁執行 WSFC 災害復原 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  
