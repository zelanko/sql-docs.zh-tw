---
title: 使用 [將資料庫加入至可用性組嚮導] （SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.adddatabasewizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], databases
ms.assetid: 81e5e36d-735d-4731-8017-2654673abb88
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0be8ed6cf2a163b3c195cfb5e4e18440549b501c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815723"
---
# <a name="use-the-add-database-to-availability-group-wizard-sql-server-management-studio"></a>使用 [將資料庫加入至可用性群組] 精靈 (SQL Server Management Studio)
  使用 [將資料庫加入至可用性群組精靈] 可將一個或多個資料庫加入現有的 AlwaysOn 可用性群組。  
  
> [!NOTE]  
>  如需使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell 加入資料庫的相關資訊，請參閱 [將資料庫加入至可用性群組 &#40;SQL Server&#41;](availability-group-add-a-database.md)。  
  
 **本主題內容：**  
  
-   **開始之前：**  
  
     [必要條件和限制](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要加入資料庫，請使用：**  [將資料庫加入可用性群組精靈 (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
 如果您從未將資料庫新增至可用性群組，請參閱[AlwaysOn 可用性群組 &#40;SQL Server&#41;的必要條件、限制和建議](prereqs-restrictions-recommendations-always-on-availability.md)中的「可用性資料庫」一節。  
  
###  <a name="prerequisites-restrictions-and-recommendations"></a><a name="Prerequisites"></a>必要條件、限制和建議  
  
-   您必須連接到裝載目前主要複本的伺服器執行個體。  
  
-   如果資料庫已加密，甚至包含資料庫加密金鑰 (DEK)，您就無法使用 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 或 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] ，將資料庫加入至可用性群組。 即使加密的資料庫已經解密，其記錄備份可能包含加密資料。 在此情況中，資料庫的完整初始資料同步處理可能會失敗。 這是因為還原記錄作業可能需要資料庫加密金鑰 (DEK) 所使用的憑證，而該憑證可能無法使用。  
  
     **若要讓解密的資料庫能夠透過精靈加入至可用性群組：**  
  
    1.  建立主要資料庫的記錄備份。  
  
    2.  建立主要資料庫的完整資料庫備份。  
  
    3.  在裝載次要複本的伺服器執行個體上還原資料庫備份。  
  
    4.  從主要資料庫建立新的記錄備份。  
  
    5.  在次要資料庫上還原這個記錄備份。  
  
-   **使用完整初始資料同步處理的必要條件**  
  
    -   每個裝載可用性群組複本之伺服器執行個體上的所有資料庫檔案路徑均須相同。  
  
    -   任何裝載次要複本的伺服器執行個體上皆不應存在主要資料庫名稱。 這表示目前還不可有任何新次要資料庫。  
  
    -   您必須指定網路共用，精靈才能建立及存取備份。 對於主要複本，用於啟動 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的帳戶必須具有網路共用的讀取與寫入檔案系統權限。 如果是次要複本，此帳戶必須有網路共用的讀取權限。  
  
     如果您無法使用精靈執行完整初始資料同步處理，則必須手動準備次要資料庫。 您可以在執行精靈前後進行這項作業。 如需詳細資訊，請參閱 [針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)中的 PowerShell，將次要資料庫聯結至 AlwaysOn 可用性群組。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="using-the-add-database-to-availability-group-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用將資料庫加入至可用性群組的 Wizard （SQL Server Management Studio）  
 **使用將資料庫加入至可用性群組精靈**  
  
1.  在 [物件總管] 中，連接到裝載可用性群組之主要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  以滑鼠右鍵按一下您要加入資料庫的可用性群組，並選取 [加入資料庫]**** 命令。 這個命令會啟動 [將資料庫加入至可用性群組] 精靈。  
  
4.  在 **[選取資料庫]** 頁面上，選取一個或多個資料庫。 如需詳細資訊，請參閱 [[選取資料庫] 頁面 &#40;新增可用性組嚮導-加入資料庫 Wizard&#41;](select-databases-page-new-availability-group-wizard-and-add-database-wizard.md)。  
  
5.  在 **[選取初始資料同步處理]** 頁面上，選擇您要如何建立新的次要資料庫並將它聯結至可用性群組。 選擇下列其中一個選項：  
  
    -   **寫**  
  
         只有在您的環境符合自動啟動初始資料同步處理的需求時，才選取此選項 (如需詳細資訊，請參閱本主題稍早的 [必要條件、限制和建議](#Prerequisites))。  
  
         如果您選取 **[完整]**，在建立可用性群組之後，精靈會嘗試將每個主要資料庫及其交易記錄備份至網路共用，並在裝載次要複本的每個伺服器執行個體上還原這些備份。 然後精靈會將每個次要資料庫聯結至可用性群組。  
  
         在 **[指定所有複本可存取的共用網路位置:]** 欄位中，指定裝載複本的所有伺服器執行個體都有讀寫存取的備份共用。 記錄備份將是記錄備份鏈結的一部分。 請適當地儲存記錄備份檔案。  
  
        > [!IMPORTANT]  
        >  如需檔案系統必要權限的資訊，請參閱本主題稍早的 [必要條件](#Prerequisites)。  
  
    -   **僅聯結**  
  
         如果您已經在將裝載次要複本的伺服器執行個體上手動備妥次要資料庫，就可以選取此選項。 然後精靈會將現有的次要資料庫聯結至可用性群組。  
  
    -   **略過初始資料同步處理**  
  
         如果要使用您自己的主要資料庫的資料庫和記錄備份，請選取此選項。 如需詳細資訊，請參閱[於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
     如需詳細資訊，請參閱[&#40;AlwaysOn 可用性群組嚮導&#41;中選取初始資料同步處理頁面](select-initial-data-synchronization-page-always-on-availability-group-wizards.md)。  
  
6.  在 **[連接到現有次要複本]** 頁面上，如果裝載此可用性群組之可用性複本的所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體都是在相同使用者帳戶下以服務方式執行，請按一下 **[全部連接]**。 如果有任何伺服器執行個體是在不同的帳戶下以服務方式執行，請按一下每個伺服器執行個體名稱右邊的個別 **[連接]** 按鈕。  
  
     如需詳細資訊，請參閱[連接到現有的次要複本頁面 &#40;新增複本嚮導和加入資料庫 wizard&#41;](connect-to-existing-secondary-replicas-page.md)。  
  
7.  **[驗證]** 頁面會驗證您在此精靈中指定的值是否符合 [新增可用性群組精靈] 的需求。 若要進行變更，您可以按 **[上一步]** 返回先前的精靈頁面，以變更一個或多個值。 然後按 **[下一步]** 返回 **[驗證]** 頁面，再按一下 **[重新執行驗證]**。  
  
     如需詳細資訊，請參閱[&#40;AlwaysOn 可用性群組嚮導&#41;的驗證頁面](validation-page-always-on-availability-group-wizards.md)。  
  
8.  在 **[摘要]** 頁面上，檢閱您為新的可用性群組的選擇。 若要進行變更，請按 **[上一步]** 返回相關頁面。 進行變更之後，請按 **[下一步]** 返回 **[摘要]** 頁面。  
  
     如需詳細資訊，請參閱[&#40;AlwaysOn 可用性群組&#41;](summary-page-always-on-availability-group-wizards.md)的 [摘要] 頁面。  
  
     如果您對所做的選擇感到滿意時，可以選擇按一下 [指令碼]，建立精靈將執行之步驟的指令碼。 然後，若要建立及設定新的可用性群組，請按一下 **[完成]**。  
  
9. **[進度]** 頁面會顯示建立可用性群組之步驟的進度 (設定端點、建立可用性群組，並將次要複本加入群組中)。  
  
     如需詳細資訊，請參閱[&#40;AlwaysOn 可用性群組嚮導&#41;的進度頁面](progress-page-always-on-availability-group-wizards.md)。  
  
10. 當這些步驟完成時， **[結果]** 頁面會顯示每個步驟的結果。 如果所有這些步驟都成功，表示新的可用性群組已完成設定。 如果任何步驟導致錯誤，您可能需要手動完成設定。 如需有關給定錯誤原因的詳細資訊，請按一下 **[結果]** 資料行中相關聯的 [錯誤] 連結。  
  
     當精靈完成時，按一下 **[關閉]** 以結束。  
  
     如需詳細資訊，請參閱[結果頁面 &#40;AlwaysOn 可用性群組精靈&#41;](results-page-always-on-availability-group-wizards.md)。  
  
11. 如果初始資料同步處理並未在所有次要資料庫上自動啟動，您需要設定任何尚未聯結的次要資料庫。 如需詳細資訊，請參閱[於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的必要條件、限制和建議&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [將資料庫新增至可用性群組 &#40;SQL Server&#41;](availability-group-add-a-database.md)   
 [在 AlwaysOn 次要資料庫上啟動資料移動 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)   
 [將資料庫加入至可用性群組 &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
  
