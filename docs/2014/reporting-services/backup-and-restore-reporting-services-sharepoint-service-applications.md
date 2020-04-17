---
title: 備份和修復報告服務 共享點服務應用程式 |微軟文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: dfb4ed77-90e5-4273-b690-89a945508ed2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 59e0de9e8ee6882b19939ef116ef4ac8023782ed
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487547"
---
# <a name="backup-and-restore-reporting-services-sharepoint-service-applications"></a>備份與還原 Reporting Services SharePoint 服務應用程式
  本主題描述如何使用 SharePoint 管理中心或 PowerShell 備份和還原 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式。 本主題包含：  
  
-   [限制事項](#bkmk_Restrictions)  
  
-   [備份服務應用程式](#bkmk_backup)  
  
-   [回復服務應用程式](#bkmk_restore)  
  
##  <a name="before-you-begin"></a><a name="bkmk_BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="bkmk_Restrictions"></a> 限制事項  
  
> [!NOTE]  
>  使用 SharePoint 備份和還原功能，就可以部分備份和還原 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式。 **需要執行其他步驟** ，且這些步驟記錄在本主題中。 目前備份程序 **不會** 將自動執行帳戶 (UEA) 或 Windows 驗證的加密金鑰和認證備份至 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料庫。  
  
###  <a name="recommendations"></a><a name="bkmk_recommendations"></a> 建議  
  
-   開始 SharePoint 備份之前，請先備份加密金鑰。 如果您未備份加密金鑰，則在還原服務應用程式之後，將無法存取加密的資料。 您將需要刪除加密的資料。  
  
-   請確認您的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式是否使用 UEA 或 Windows 驗證進行資料庫存取。 如果是使用其中一種方式，請確定正確的認證為何，如此就能在還原程序之後正確設定服務應用程式。  
  
-   檢閱 SharePoint 備份記錄確實是在備份檔案所在的資料夾中建立。 這個檔案通常命名為 **spbackup.log**  
  
##  <a name="backup-the-service-application"></a><a name="bkmk_backup"></a>備份服務應用程式  
 依序完成下列步驟：  
  
1.  備份加密金鑰  
  
2.  備份服務應用程式  
  
3.  確認您的服務應用程式是否使用 UEA 或 Windows 驗證進行資料庫存取。 如果是的話，請記下認證，以便在還原服務應用程式之後使用認證進行設定。  
  
### <a name="backup-the-encryption-keys-using-central-administration"></a>使用管理中心備份加密金鑰  
 如需備份 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 加密金鑰的資訊，請參閱[管理 Reporting Services SharePoint 服務應用程式](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)的＜加密金鑰＞一節。  
  
###  <a name="backup-the-service-application-using-sharepoint-central-administration"></a><a name="bkmk_centraladmin"></a>使用 SharePoint 管理中心備份服務應用程式  
 若要備份服務應用程式，請完成下列步驟：  
  
1.  在 [SharePoint 管理中心] 中，按一下 **[備份與還原]** 群組中的 **[執行備份]** 。  
  
2.  在 **[共用服務]** 節點底下，展開 **[共用服務應用程式]** ，然後選取您的服務應用程式。 其類型會是 **[SQL Server Reporting Services 服務應用程式]**。  
  
3.  按 [下一步]  。  
  
4.  輸入 **[備份位置:]** 的路徑，然後按一下 **[開始備份]**。  
  
5.  重複上述程序，但是不要選取服務應用程式，而是展開 **[共用服務 Proxy]** 節點，然後選取服務應用程式 Proxy。 其類型會是 **[SQL Server Reporting Services 服務應用程式 Proxy]**。  
  
 如需詳細資訊，請參閱 SharePoint 文件中的下列主題：  
  
 SharePoint 文件中的[備份服務應用程式 (SharePoint Foundation 2010)](https://msdn.microsoft.com/library/ee748601.aspx)。  
  
 [備份服務應用程式 (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>驗證執行帳戶和資料庫驗證  
 **執行帳戶** ：若要驗證您的服務應用程式是否使用執行帳戶：  
  
1.  在 SharePoint 管理中心中,單擊 **「在應用程式管理**組中**管理服務應用程式**」。  
  
2.  按一下服務應用程式的名稱,然後單擊 SharePoint 功能區中的 **「管理**」。  
  
3.  按一下 **[執行帳戶]**。  
  
4.  如果設定了執行帳戶，則在還原服務應用程式備份時需要知道認證。 如果不知道正確的認證，請不要進行備份和還原程序。  
  
 **資料庫驗證** ：若要確認您的服務應用程式是否使用 Windows 驗證進行資料庫驗證：  
  
1.  在 SharePoint 管理中心中,單擊 **「在應用程式管理**組中**管理服務應用程式**」。  
  
2.  按一下服務應用程式的名稱，然後按一下 SharePoint 功能區中的 **[屬性]** 。  
  
3.  檢閱 **[Reporting Services (SSRS) 服務資料庫]** 區段。  
  
4.  如果設定了 Windows 驗證，則您必須知道認證，才能在還原之後設定服務應用程式。 如果不知道正確的認證，請不要進行備份和還原程序。  
  
##  <a name="restore-the-service-application"></a><a name="bkmk_restore"></a>回復服務應用程式  
 依序完成下列步驟：  
  
1.  還原 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式。  
  
2.  還原加密金鑰  
  
3.  如果您的服務應用程式使用執行帳戶或 Windows 驗證進行資料庫存取，請設定認證。  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>使用 SharePoint 管理中心還原服務應用程式  
  
1.  在 [SharePoint 管理中心] 中，按一下 **[備份與還原]** 群組中的 **[從備份還原]** 。  
  
2.  在 **[備份目錄位置]** 方塊中輸入備份檔案的路徑，然後按一下 **[重新整理]**。  
  
3.  從 **[上層元件]** 清單中選取服務應用程式備份，然後按 **[下一步]**。  
  
4.  選取您的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 應用程式，然後按 **[下一步]**。  
  
5.  在 **[登錄名稱與密碼]** 區段中，輸入登入名稱的密碼。 [登入名稱] 方塊應填入服務應用程式在備份之前使用的登入。  
  
6.  按一下 **[開始還原]**。  
  
7.  重複上述程序，但是不要還原服務應用程式，而是展開 **[共用服務]** 節點，然後展開 **[共用服務應用程式]** 節點。  
  
 如需詳細資訊，請參閱 SharePoint 文件中的下列主題：  
  
 [還原服務應用程式 (SharePoint Foundation 2010)](https://msdn.microsoft.com/library/ee748615.aspx)。  
  
 [Restore a service application (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx)(還原服務應用程式 (SharePoint Server 2010))。  
  
### <a name="restore-the-encryption-keys-using-central-administration"></a>使用管理中心還原加密金鑰  
 如需還原 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 加密金鑰的資訊，請參閱[管理 Reporting Services SharePoint 服務應用程式](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)的＜加密金鑰＞一節。  
  
### <a name="configure-the-execution-account-and-database-authentication"></a>設定執行帳戶和資料庫驗證  
 **執行帳戶** ：如果您的服務應用程式使用執行帳戶，請完成下列步驟設定該帳戶：  
  
1.  在 SharePoint 管理中心中,單擊 **「在應用程式管理**組中**管理服務應用程式**」。  
  
2.  按一下服務應用程式的名稱,然後單擊 SharePoint 功能區中的 **「管理**」。  
  
3.  按一下 **[執行帳戶]**。  
  
4.  輸入帳戶、密碼，然後選取 **[指定執行帳戶]** 方塊。  
  
5.  按一下 [確定]  。  
  
 **資料庫驗證** ：如果您的服務應用程式使用 Windows 驗證進行資料庫驗證，請完成下列步驟：  
  
1.  在 SharePoint 管理中心中,單擊 **「在應用程式管理**組中**管理服務應用程式**」。  
  
2.  按一下服務應用程式的名稱，然後按一下 SharePoint 功能區中的 **[屬性]** 。  
  
3.  檢閱 **[Reporting Services (SSRS) 服務資料庫]** 區段。  
  
4.  選取 **[Windows 驗證]**。  
  
5.  輸入帳戶和密碼。 選取 **[當做 Windows 認證使用]** (如果適用)。  
  
6.  單擊 **"確定"**  
  
  
