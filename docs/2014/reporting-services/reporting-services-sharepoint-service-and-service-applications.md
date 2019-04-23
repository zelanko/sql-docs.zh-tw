---
title: Reporting Services SharePoint 服務和服務應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 501aa9ee-8c13-458c-bf6f-24e00c82681b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 40bfd5e68aa8c27ee0024147eeadc99f0da91ce2
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59954214"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Reporting Services SharePoint 服務和服務應用程式
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式是以 SharePoint 服務架構為基礎進行架構，並且利用 SharePoint 服務和一對多服務應用程式。 建立服務應用程式可讓服務變成可用，並產生服務應用程式資料庫。 您可以建立多個 Reporting Services 服務應用程式，但是一個服務應用程式就足以應付大部分的部署狀況。  
  
 本主題涵蓋下列資訊：  
  
-   [建立 Reporting Services 服務應用程式](#bkmk_createapp)  
  
-   [修改服務應用程式與 Proxy 群組的關聯](#bkmk_associations)  
  
-   [編輯服務應用程式屬性](#bkmk_editserviceapplication)  
  
-   [使用 PowerShell 建立 Reporting Services 服務應用程式](#bkmk_powershell_create_ssrs_serviceapp)  
  
-   [相關工作](#bkmk_related)  
  
##  <a name="bkmk_createapp"></a> 建立 Reporting Services 服務應用程式  
 您可以使用 SharePoint 管理中心或 PowerShell 指令碼建立 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式。 如需使用 SharePoint 管理中心的詳細資訊，請參閱[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)中的＜建立 Reporting Services 服務應用程式＞一節。 如需建立服務應用程式的範例 PowerShell 指令碼，請參閱本主題稍後的＜PowerShell＞一節。  
  
##  <a name="bkmk_associations"></a> 修改服務應用程式與 Proxy 群組的關聯  
 建立服務應用程式的 [新增] 頁面包含 **[Web 應用程式關聯]** 區段。 此區段可讓您在建立服務應用程式時產生關聯。 使用下列步驟變更關聯並將客戶組態指派至服務應用程式。 您也可以使用相同的一般程序將 Proxy 加入至預設群組，而不是將服務應用程式的關聯變更為自訂群組。  
  
1.  在 [SharePoint 管理中心] 的 [應用程式管理] 中，按一下 **[設定服務應用程式關聯]**。  
  
2.  在 [服務應用程式關聯] 頁面上，將檢視切換至 **[服務應用程式]**。  
  
3.  尋找並按一下新的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式的名稱。 您也可以按一下應用程式 Proxy 群組名稱 **default** ，將 Proxy 加入至預設群組，而不要完成下列步驟。  
  
4.  在 **[編輯下列連線群組]** 選取方塊中選取 **[自訂]**。  
  
5.  核取您的 Proxy 的方塊，然後按一下 **[確定]**。  
  
##  <a name="bkmk_editserviceapplication"></a> 編輯服務應用程式屬性  
 您可以再次開啟服務應用程式的屬性頁來修改屬性。  
  
1.  在 [SharePoint 管理中心] 的 [應用程式管理] 群組中，按一下 **[管理服務應用程式]**。  
  
2.  按一下類型資料行選取整個資料列，藉此選取服務應用程式。 如果您按一下應用程式的名稱，則會開啟服務的 [管理] 選項頁面，而不是開啟服務應用程式的屬性。  
  
3.  在 [服務應用程式] 功能區中，按一下 **[內容]**。  
  
##  <a name="bkmk_powershell_create_ssrs_serviceapp"></a> 使用 PowerShell 建立 Reporting Services 服務應用程式  
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
  
##  <a name="bkmk_related"></a> 相關工作  
  
|工作|連結|  
|----------|----------|  
|管理服務應用程式的設定。|[管理 Reporting Services SharePoint 服務應用程式](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)|  
|備份和還原服務應用程式及相關元件，例如加密金鑰和 Proxy。|[備份與還原 Reporting Services SharePoint 服務應用程式](../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  
  
  
