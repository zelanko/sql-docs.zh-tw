---
title: 解除安裝 Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 5c764a00-d4bc-465d-b32e-e4efce052ce4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 16466f509383ec407dafcd5a9cf61b324a7c4b52
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "71951571"
---
# <a name="uninstall-reporting-services"></a>解除安裝 Reporting Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會移除您已建立的內容或是您已修改的組態。 不過，如果有解除安裝完成之後需要的內容，建議您先建立內容的複本，然後再開始進行解除安裝程序。  
  
## <a name="uninstall-sharepoint-mode"></a>解除安裝 SharePoint 模式  
 解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式時會一併移除下列各項：  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務和服務 Proxy。  
  
-   用於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝的檔案。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式則不會移除。 如果您不再需要服務應用程式，可以使用 Windows PowerShell 或 SharePoint 管理中心刪除它們。  
  
 報表項目和相關中繼資料則不會移除。 這項資訊包含在與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式相關的內容和組態資料庫中。 資料庫不會移除，而且您可以手動將資料庫移轉至 SharePoint 模式下的另一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝。 如果您不再需要資訊，請刪除資料庫。 如需詳細資訊，請參閱＜ [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)＞。  
  
 以下是三個不會移除之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料庫的範例名稱。  
  
-   **報表伺服器資料庫：** ReportingService_7f616e2d253040e8ab5653b3c09a065e  
  
-   **報表伺服器暫存資料庫：** ReportingService_7f616e2d253040e8ab5653b3c09a065eTempDB  
  
-   **報表伺服器警示資料庫：** ReportingService_7f616e2d253040e8ab5653b3c09a065e_Alerting  
  
### <a name="uninstall-the-add-in-for-sharepoint-products"></a>解除安裝適用於 SharePoint 產品的增益集  
 當您從電腦解除安裝增益集時，可以選擇只從伺服器陣列解除安裝檔案，或是一併移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能。 如需解除安裝 SharePoint 產品 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的詳細資訊，請參閱 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  
  
## <a name="uninstall-native-mode"></a>解除安裝原生模式  
 當您解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式時，安裝之後所 **建立** 或 **修改** 的任何內容都會保持原狀。 例如，資料庫檔案、記錄檔、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態檔和內容項目 (如報表和資料來源檔案)。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是執行個體功能，因此不會列在 Windows [控制台] 的 [程式和功能] 中。 若要解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式：  
  
1.  在 Windows [控制台] 中，按一下 **[程式和功能]** 。  
  
2.  在 [程式和功能]  中，選取 [Microsoft SQL Server 2016]  。  
  
3.  在解除安裝精靈中，選取包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體功能 **RS**的執行個體。  
  
     ![rs_nativemode_uninstall_selectinstance](../../sql-server/install/media/rs-nativemode-uninstall-selectinstance.gif "rs_nativemode_uninstall_selectinstance")  
  
4.  當您選取執行個體之後，請選取 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能。  
  
     ![rs_nativemode_uninstall_selectfeatures](../../sql-server/install/media/rs-nativemode-uninstall-selectfeatures.gif "rs_nativemode_uninstall_selectfeatures")  
  
5.  完成精靈。  
  
## <a name="see-also"></a>另請參閱  
 [解除安裝現有的 SQL Server 執行個體 &#40;Setup&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [安裝或解除安裝 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
