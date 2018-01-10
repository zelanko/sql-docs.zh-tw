---
title: "安裝報表產生器 | Microsoft Docs"
ms.custom: 
ms.date: 09/22/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
caps.latest.revision: "20"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 395ec440e3cae0ac4013edc9c35af36e32a73d0c
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="install-report-builder"></a>Install Report Builder
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 是一種獨立式應用程式，由您或系統管理員安裝在電腦上。 您可以透過 Microsoft 下載中心、 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器，或整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 SharePoint 網站進行安裝。  
  
 系統管理員通常會安裝及設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、授與從入口網站下載 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的權限，以及管理儲存到報表伺服器之報表、報表組件和共用資料集的資料夾和權限。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理的詳細資訊，請參閱 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
## <a name="install-includessrbnoversionincludesssrbnoversion-mdmd-from--a--web-portal-or-sharepoint-library"></a>從入口網站或 SharePoint 文件庫安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 
  
 您可以從 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 入口網站或整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 SharePoint 網站來啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 如需資訊，請參閱 [啟動報表產生器](../../reporting-services/report-builder/start-report-builder.md)。  
  
### <a name="sharepoint-site-integrated-with-includessrsnoversionincludesssrsnoversion-mdmd"></a>整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 在整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 SharePoint 網站上，如果 [新增文件]  功能表未列出 [報表產生器報表] 、[報表產生器模型] 和 [報表資料來源] ，則必須將其內容類型加入 SharePoint 文件庫。 如需詳細資訊，請參閱 [將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
 
## <a name="install-includessrbnoversionincludesssrbnoversion-mdmd-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 
  
 系統管理員也可以使用 System Center Configuration Manager 這類軟體，將此程式發送至您的電腦。 若要了解如何使用特定軟體來安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]，請參閱軟體的文件集。 如需詳細資訊，請參閱 [System Center Configuration Manager 網站](https://www.microsoft.com/en-us/cloud-platform/system-center-configuration-manager)。  
  
> [!IMPORTANT]  
>  Windows Vista 和 Windows 7 安全性功能需要更高的權限才能執行命令列作業，並且會提示執行命令列的權限。 安裝不是無訊息的。 若要進行無訊息安裝，您必須以管理員的身分執行命令列。  
  
## <a name="system-requirements"></a>系統需求
  
 請參閱 Microsoft 下載中心 **報表產生器下載頁面** 的 [System Requirements (系統需求)](http://go.microsoft.com/fwlink/?LinkID=734968) 區段。
  
##  <a name="download"></a> 若要從下載網站安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
1.  在 [Microsoft 下載中心的報表產生器頁面](http://go.microsoft.com/fwlink/?LinkID=734968) ，按一下 [下載] 。  
  
2.  完成下載 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 之後，按一下 [執行]。  
  
     隨即啟動 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 精靈。  
  
3.  接受授權合約條款，然後按一下 [下一步] 。  
  
4.  在 **[預設的目標伺服器]** 頁面上，選擇性地提供目標報表伺服器的 URL (如果它與預設值不同的話)。 按 [下一步] 。  
  
    > [!NOTE]  
    >  如果您計畫在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 連接至報表伺服器時使用它，此時提供伺服器的 URL 比較方便。 您也可以透過 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的 [選項] 對話方塊執行此作業。  
  
5.  按一下 [安裝] 完成 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的安裝程序。  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversion-mdmd-from-a-share"></a>若要從共用安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
1.  如需在本機電腦上安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 所必須執行之 ReportBuilder3.msi 的位置，請連絡系統管理員。  
  
2.  瀏覽並找出 ReportBuilder3.msi ( [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]的 Windows InstalleR 封裝 (MSI))，然後按一下此檔案。  
  
     隨即啟動 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 精靈。  
  
3.  完成 [To install Report Builder from the download site](#download)的其餘步驟。  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversion-mdmd-from-the-command-line"></a>若要從命令列安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 

 您也可以執行 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的命令列安裝，並提供引數來自訂安裝。 除了標準的 MSI 內建參數以外，您還可以使用 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 所提供的自訂參數：RBINSTALLDIR 和 REPORTSERVERURL。 RBINSTALLDIR 會指定 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]的根安裝資料夾。 REPORTSERVERURL 會指定 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 用來在伺服器上儲存報表的預設報表伺服器。  
  
 如果您想要進行完全無訊息的安裝 (完全沒有使用者介面互動)，請指定 **/quiet** 選項。 根據設計，quiet 選項旗標會隱藏安裝錯誤。 因此，當您使用 quiet 選項時，建議您加入 **/l** 選項 (指定記錄)。   
  
1.  在 [Microsoft 下載中心的報表產生器頁面](http://go.microsoft.com/fwlink/?LinkID=734968)，按一下 [下載]。  
  
2.  完成下載 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 之後，按一下 [儲存]。  
  
3.  在 **[開始]** 功能表上，按一下 **[執行]**。  
  
4.  在 [開啟]  方塊中輸入 **cmd.**。  
  
5.  在 [命令提示字元] 視窗中，瀏覽至儲存 ReportBuilder3.msi 的資料夾。  
  
6.  輸入下列格式的命令：  
  
     `msiexec/i ReportBuilder3.msi /option [value] [/option [value]]`  
  
     安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的兩個專屬選項是：RBINSTALLDIR 和 REPORTSERVERURL。 您不需要在命令列中包含這些引數。 以下為基準命令：  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  若要執行命令，請按 Enter 鍵。  
  
## <a name="set-includessrbnoversionincludesssrbnoversion-mdmd-defaults"></a>設定 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 預設值  
  
-   安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]之後，您可以設定一些預設選項。 按一下 [檔案] > [選項]。  
  
     設定預設 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站或 SharePoint 網站最為實用。 如需詳細資訊，請參閱 [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md)。  
  
-   按一下 [報表產生器]  。  
  
     若您在現有伺服器清單中沒有看到報表伺服器，請關閉 [開啟報表] 對話方塊，然後按一下 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 底部的 [連線]，以連線至伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [啟動報表產生器](../../reporting-services/report-builder/start-report-builder.md)   
 [將報表產生器解除安裝](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
  
