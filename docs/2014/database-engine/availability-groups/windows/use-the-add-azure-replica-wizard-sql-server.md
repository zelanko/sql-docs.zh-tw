---
title: 使用新增 Azure 複本精靈 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90418193ac869641a20f8b0f684fc43dd46712f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176001"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>使用加入 Azure 複本精靈 (SQL Server)
  使用 [加入 Azure 複本] 嚮導，協助您在混合式 IT 中建立新的 Azure VM，並將其設定為新的或現有 AlwaysOn 可用性群組的次要複本。  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **使用下列方法加入複本：**  [加入 Azure 複本精靈 (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
 如果您從未將任何可用性複本新增至可用性群組，請參閱[AlwaysOn 可用性群組 &#40;SQL Server&#41;的必要條件、限制和建議](prereqs-restrictions-recommendations-always-on-availability.md)中的「伺服器實例」和「可用性群組和複本」小節。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   您必須連接到裝載目前主要複本的伺服器執行個體。  
  
-   您必須擁有混合式 IT 環境，其中的內部部署子網路具有 Azure 的站對站 VPN。 如需詳細資訊，請參閱 [使用 Azure 傳統入口網站建立具有站對站 VPN 連線的虛擬網路](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create)。  
  
-   您的可用性群組必須包含內部部署可用性複本。  
  
-   如果可用性群組接聽程式的用戶端想要在可用性群組容錯移轉至 Azure 複本時維持接聽程式的連線能力，它們就必須具有網際網路的連線能力。  
  
-   **使用完整初始資料同步處理的必要條件** ：您需要指定網路共用，才能讓精靈建立及存取備份。 對於主要複本，用於啟動 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的帳戶必須具有網路共用的讀取與寫入檔案系統權限。 如果是次要複本，此帳戶必須有網路共用的讀取權限。  
  
     如果您無法使用精靈執行完整初始資料同步處理，則必須手動準備次要資料庫。 您可以在執行精靈前後進行這項作業。 如需詳細資訊，請參閱 [針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)中的 PowerShell，將次要資料庫聯結至 AlwaysOn 可用性群組。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 請參閱 [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="using-the-add-azure-replica-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用加入 Azure 複本 Wizard （SQL Server Management Studio）  
 您可以從 [指定複本頁面](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)啟動 [加入 Azure 複本精靈]。 存取這個頁面的方式有兩種：  
  
-   [使用可用性群組精靈 &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用 [將複本加入可用性群組中精靈] &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 一旦您啟動 [加入 Azure 複本精靈] 之後，請遵循下列步驟進行：  
  
1.  首先，下載您的 Azure 訂用帳戶的管理憑證。 按一下 [下載]**** 開啟登入頁面。  
  
2.  在登入頁面中，登入您的 Azure 訂用帳戶。 一旦您登入之後，此精靈就會將管理憑證安裝到本機電腦上。 當您再次使用此精靈時，就會自動載入這個管理憑證。 如果您已下載多個管理憑證，可以按一下 **...** 按鈕選取您想要使用的憑證。  
  
3.  接著，按一下 **[連接]**，連接到您的訂用帳戶。 一旦您連線之後，下拉式清單就會填入您的 Azure 參數，例如 [虛擬網路]**** 和 [虛擬網路子網路]****。  
  
4.  針對將裝載新次要複本的 Azure VM 指定設定：  
  
     Image  
     要用於 Azure VM 的 SQL Server 映像名稱  
  
     VM 大小  
     Azure VM 的大小  
  
     虛擬機器名稱  
     Azure VM 的 DNS 名稱  
  
     VM 使用者名稱  
     Azure VM 預設系統管理員的使用者名稱  
  
     VM 系統管理員密碼 (和確認密碼)  
     Azure VM 預設系統管理員的密碼  
  
     虛擬網路  
     要放置 Azure VM 的虛擬網路  
  
     虛擬網路子網路  
     要放置 Azure VM 的虛擬網路子網路  
  
     網域  
     要加入 Azure VM 的 Active Directory (AD) 網域  
  
     網域使用者名稱  
     用來將 Azure VM 加入至網域的 AD 使用者名稱  
  
     密碼  
     用來將 Azure VM 加入至網域的密碼  
  
5.  按一下 **[確定]** 認可您的設定並結束 [加入 Azure 複本精靈]。  
  
6.  繼續針對 [指定複本頁面](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) 進行其餘組態設定步驟，就像設定任何新的複本一樣。  
  
     當您完成 [可用性群組嚮導] 或 [將複本加入至可用性組嚮導] 之後，設定程式會執行 Azure 中的所有作業來建立新的 VM、將它加入 AD 網域、將它新增至 Windows 叢集、啟用 AlwaysOn 高可用性，並將新的複本加入至可用性群組。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [將次要複本加入至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的必要條件、限制和建議&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [將次要複本新增至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
