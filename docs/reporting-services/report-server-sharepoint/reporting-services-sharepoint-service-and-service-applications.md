---
title: Reporting Services SharePoint 服務和服務應用程式 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1dfe62ba964b05f069009b51ddf62f376c12c906
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580538"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Reporting Services SharePoint 服務和服務應用程式

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services SharePoint 模式是以 SharePoint 服務架構為基礎進行架構，並且利用 SharePoint 服務和一對多服務應用程式。 建立服務應用程式可讓服務變成可用，並產生服務應用程式資料庫。 您可以建立多個 Reporting Services 服務應用程式，但是一個服務應用程式就足以應付大部分的部署狀況。  

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。
  
## <a name="creating-a-reporting-services-service-application"></a>建立 Reporting Services 服務應用程式

 您可以使用 SharePoint 管理中心或 PowerShell 指令碼建立 Reporting Services 服務應用程式。 如需使用 SharePoint 管理中心的詳細資訊，請參閱[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)中的＜建立 Reporting Services 服務應用程式＞一節。 如需建立服務應用程式的範例 PowerShell 指令碼，請參閱本主題稍後的＜PowerShell＞一節。  
  
## <a name="modify-the-associations-of-the-service-application-with-a-proxy-group"></a>修改服務應用程式與 Proxy 群組的關聯

 建立服務應用程式的 [新增] 頁面包含 **[Web 應用程式關聯]** 區段。 此區段可讓您在建立服務應用程式時產生關聯。 使用下列步驟變更關聯並將客戶組態指派至服務應用程式。 您也可以使用相同的一般程序將 Proxy 加入至預設群組，而不是將服務應用程式的關聯變更為自訂群組。  
  
1.  在 [SharePoint 管理中心] 的 [應用程式管理] 中，按一下 **[設定服務應用程式關聯]** 。  
  
2.  在 [服務應用程式關聯] 頁面上，將檢視切換至 **[服務應用程式]** 。  
  
3.  尋找並按一下新的 Reporting Services 服務應用程式的名稱。 您也可以按一下應用程式 Proxy 群組名稱 **default** ，將 Proxy 加入至預設群組，而不要完成下列步驟。  
  
4.  在 **[編輯下列連線群組]** 選取方塊中選取 **[自訂]** 。  
  
5.  核取您的 Proxy 的方塊，然後按一下 **[確定]** 。  
  
## <a name="edit-service-application-properties"></a>編輯服務應用程式屬性

 您可以再次開啟服務應用程式的屬性頁來修改屬性。  
  
1.  在 [SharePoint 管理中心] 的 [應用程式管理] 群組中，按一下 **[管理服務應用程式]** 。  
  
2.  按一下類型資料行選取整個資料列，藉此選取服務應用程式。 如果您按一下應用程式的名稱，則會開啟服務的 [管理] 選項頁面，而不是開啟服務應用程式的屬性。  
  
3.  在 [服務應用程式] 功能區中，按一下 **[內容]** 。  
  
## <a name="create-a-reporting-services-service-application-using-powershell"></a>使用 PowerShell 建立 Reporting Services 服務應用程式

 您可以使用 PowerShell 建立服務應用程式和 Proxy。 下方範例是假設您知道要設定服務應用程式使用哪個應用程式集區。  
  
1.  將應用程式集區名稱的應用程式集區物件加入至要傳遞到 [新增] 動作的變數中。  
  
    ```  
    $appPoolName = get-spserviceapplicationpool "<application pool name>"  
    ```  
  
2.  使用您提供的名稱與應用程式集區名稱建立服務應用程式。  
  
    ```  
    New-SPRSServiceApplication -Name 'MyServiceApplication' -ApplicationPool $appPoolName -DatabaseName 'MyServiceApplicationDatabase' -DatabaseServer '<Server Name>'  
    ```  
  
3.  取得新的服務應用程式物件，並且將物件以管道傳送至 Pipe 新 Proxy Cmdlet。  
  
    ```  
    Get-SPRSServiceApplication -name MyServiceApplication | New-SPRSServiceApplicationProxy "MyServiceApplicationProxy"  
    ```  
  
## <a name="related-tasks"></a>相關工作
  
|Task|連結|  
|----------|----------|  
|管理服務應用程式的設定。|[管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|  
|備份和還原服務應用程式及相關元件，例如加密金鑰和 Proxy。|[備份與還原 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
