---
title: "備份與還原 Reporting Services SharePoint 服務應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: b6dcd64d6f9662ae592474053e6cc9bbce53a83e
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>備份與還原 Reporting Services SharePoint 服務應用程式

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

本主題描述如何備份和還原[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務應用程式使用 SharePoint 管理中心或 PowerShell。

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

## <a name="before-you-begin"></a>開始之前

### <a name="limitations-and-restrictions"></a>限制事項

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務應用程式可以部分備份和還原使用 SharePoint 備份和還原功能。 **需要執行其他步驟** ，且這些步驟記錄在本主題中。 目前備份的程序**不**備份加密金鑰和認證自動的執行帳戶 (UEA) 或 windows 驗證來[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]資料庫。

### <a name="recommendations"></a>建議
  
-   開始 SharePoint 備份之前，備份加密金鑰。 如果您沒有備份的加密金鑰，然後您將無法存取加密的資料在還原服務應用程式之後。 您將需要刪除加密的資料。  
  
-   請確認您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式是否使用 UEA 或 Windows 驗證進行資料庫存取。 如果是使用其中一種方式，請確定正確的認證為何，如此就能在還原程序之後正確設定服務應用程式。  
  
-   檢閱 SharePoint 備份記錄檔會在備份檔案的相同資料夾中建立。 這個檔案通常命名為 **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>備份服務應用程式

 依序完成下列步驟：  
  
1.  備份加密金鑰  
  
2.  備份服務應用程式  
  
3.  確認您的服務應用程式是否使用 UEA 或 Windows 驗證進行資料庫存取。 如果是的話，請記下認證，以便在還原服務應用程式之後使用認證進行設定。  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>備份加密金鑰，使用 SharePoint 管理中心

如需備份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰的資訊，請參閱 [管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)的＜加密金鑰＞一節。  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>備份服務應用程式使用 SharePoint 管理中心

若要備份服務應用程式，請完成下列步驟：  
  
1.  在 SharePoint 管理中心 中選取**執行備份**中**備份和還原**群組。  
  
2.  在 **[共用服務]** 節點底下，展開 **[共用服務應用程式]** ，然後選取您的服務應用程式。 其類型會是 **[SQL Server Reporting Services 服務應用程式]**。  
  
3.  選取 **[下一步]**。  
  
4.  輸入的路徑**備份位置：**選取**開始備份**  
  
5.  重複上述程序，但是不要選取服務應用程式，而是展開 **[共用服務 Proxy]** 節點，然後選取服務應用程式 Proxy。 其類型會是 **[SQL Server Reporting Services 服務應用程式 Proxy]**。  
  
 如需詳細資訊，請參閱 SharePoint 文件中的下列主題：  
  
 SharePoint 文件中的[備份服務應用程式 (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748601.aspx)。  
  
 [備份服務應用程式 (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>驗證執行帳戶和資料庫驗證

 **執行帳戶** ：若要驗證您的服務應用程式是否使用執行帳戶：  
  
1.  在 SharePoint 管理中心內，選取**管理服務應用程式**中**應用程式管理**群組。  
  
2.  選取服務應用程式的名稱，然後選取**管理**SharePoint 功能區中。  
  
3.  選取**執行帳戶**。  
  
4.  如果設定了執行帳戶，則在還原服務應用程式備份時需要知道認證。 如果不知道正確的認證，請不要進行備份和還原程序。  
  
 **資料庫驗證** ：若要確認您的服務應用程式是否使用 Windows 驗證進行資料庫驗證：  
  
1.  在 SharePoint 管理中心內，選取**管理服務應用程式**中**應用程式管理**群組。  
  
2.  選取服務應用程式的名稱，然後選取**屬性**SharePoint 功能區中。  
  
3.  檢閱 **[Reporting Services (SSRS) 服務資料庫]** 區段。  
  
4.  如果設定了 Windows 驗證，則您必須知道認證，才能在還原之後設定服務應用程式。 如果不知道正確的認證，請不要進行備份和還原程序。  
  
## <a name="restore-the-service-application"></a>還原服務應用程式

 依序完成下列步驟：  
  
1.  還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。  
  
2.  還原加密金鑰  
  
3.  如果您的服務應用程式使用執行帳戶或 Windows 驗證進行資料庫存取，請設定認證。  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>還原服務應用程式使用 SharePoint 管理中心
  
1.  在 SharePoint 管理中心 中選取**從備份還原**中**備份和還原**群組。  
  
2.  輸入您的備份檔案中的路徑**備份目錄位置**方塊，然後選取**重新整理**。  
  
3.  選取服務應用程式備份從**上層元件**清單，然後選取 **下一步**。  
  
4.  選取您[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]應用程式，然後選取**下一步**。  
  
5.  在 **[登錄名稱與密碼]** 區段中，輸入登入名稱的密碼。 登入名稱 方塊應填入服務應用程式上一步之前使用上的登入。  
  
6.  選取**開始還原**。  
  
7.  重複上述程序，但是不要還原服務應用程式，而是展開 **[共用服務]** 節點，然後展開 **[共用服務應用程式]** 節點。  
  
 如需詳細資訊，請參閱 SharePoint 文件中的下列主題：  
  
 [還原服務應用程式 (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx)。  
  
 [Restore a service application (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx)(還原服務應用程式 (SharePoint Server 2010))。  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>還原加密金鑰，使用 SharePoint 管理中心

 如需還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰的資訊，請參閱 [管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)的＜加密金鑰＞一節。  

### <a name="configure-the-execution-account-and-database-authentication"></a>設定執行帳戶和資料庫驗證

 **執行帳戶** ：如果您的服務應用程式使用執行帳戶，請完成下列步驟設定該帳戶：  
  
1.  在 SharePoint 管理中心內，選取**管理服務應用程式**中**應用程式管理**群組。  
  
2.  選取服務應用程式的名稱，然後選取**管理**SharePoint 功能區中。  
  
3.  選取**執行帳戶**。  
  
4.  輸入帳戶、密碼，然後選取 **[指定執行帳戶]** 方塊。  
  
5.  選取 [確定]。  
  
 **資料庫驗證** ：如果您的服務應用程式使用 Windows 驗證進行資料庫驗證，請完成下列步驟：  
  
1.  在 SharePoint 管理中心 中選取**管理服務應用程式**中**應用程式管理**群組。  
  
2.  選取服務應用程式的名稱，然後選取**屬性**SharePoint 功能區中。  
  
3.  檢閱 **[Reporting Services (SSRS) 服務資料庫]** 區段。  
  
4.  選取 **[Windows 驗證]**。  
  
5.  輸入帳戶和密碼。 選取 **[當做 Windows 認證使用]** (如果適用)。  
  
6.  選取**[確定]**

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

