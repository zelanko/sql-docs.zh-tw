---
title: 安裝報表產生器 | Microsoft Docs
description: 報表產生器是一種獨立式應用程式，由您或系統管理員安裝在電腦上。
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d256ac7cc7f7925ad307c527378abcca5b6d121f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76971379"
---
# <a name="install-report-builder"></a>安裝報表產生器

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]是一種獨立式應用程式，由您或系統管理員安裝在電腦上。 您可以透過 Microsoft 下載中心、 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器，或整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 SharePoint 網站進行安裝。  

> [!NOTE]
> 要改為尋找 Power BI Report Builder 的安裝資訊嗎？ 前往下載中心的 [Microsoft Power BI Report Builder](https://www.microsoft.com/download/details.aspx?id=58158) 頁面。 

 系統管理員通常會安裝及設定[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、授與從入口網站下載[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]的權限，以及管理儲存到報表伺服器之報表、報表組件和共用資料集的資料夾和權限。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理的詳細資訊，請參閱 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
## <a name="install-ssrbnoversion-from--a--web-portal-or-sharepoint-library"></a>從 Web 入口網站或 SharePoint 文件庫安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。
  
 您可以從 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 入口網站或整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 SharePoint 網站來啟動 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]。 如需資訊，請參閱 [啟動報表產生器](../../reporting-services/report-builder/start-report-builder.md)。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
### <a name="sharepoint-site-integrated-with-ssrsnoversion"></a>整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 在整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 SharePoint 網站上，如果 [新增文件]  功能表未列出 [報表產生器報表]  、[報表產生器模型]  和 [報表資料來源]  ，則必須將其內容類型加入 SharePoint 文件庫。 如需詳細資訊，請參閱 [將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  

::: moniker-end
 
## <a name="install-ssrbnoversion-with-microsoft-endpoint-configuration-manager"></a>使用 Microsoft Endpoint Configuration Manager 安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 
  
 系統管理員也可以使用 Microsoft Endpoint Configuration Manager 這類軟體，將該程式推送至您的電腦。 若要了解如何使用特定軟體來安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]，請參閱軟體的文件集。 如需詳細資訊，請參閱 [Microsoft Endpoint Configuration Manager 文件](https://docs.microsoft.com/configmgr/)。  
  
> [!IMPORTANT]  
>  Windows Vista 和 Windows 7 安全性功能需要更高的權限才能執行命令列作業，並且會提示執行命令列的權限。 安裝不是無訊息的。 若要進行無訊息安裝，您必須以管理員的身分執行命令列。  
  
## <a name="system-requirements"></a>系統需求
  
 請參閱 Microsoft 下載中心 **報表產生器下載頁面** 的 [System Requirements (系統需求)](https://go.microsoft.com/fwlink/?LinkID=734968) 區段。
  
##  <a name="to-install-ssrbnoversion-from-the-download-site"></a><a name="download"></a> 從下載網站安裝[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]  
  
1.  在 [Microsoft 下載中心的報表產生器頁面](https://go.microsoft.com/fwlink/?LinkID=734968) ，按一下 [下載]  。  
  
2.  完成下載 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 之後，按一下 [執行]  。  
  
     隨即啟動 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 精靈。  
  
3.  接受授權合約條款，然後按一下 [下一步]  。  
  
4.  在 **[預設的目標伺服器]** 頁面上，選擇性地提供目標報表伺服器的 URL (如果它與預設值不同的話)。 按 [下一步]  。  
  
    > [!NOTE]  
    >  如果您計畫在[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]連線至報表伺服器時使用它，此時提供伺服器的 URL 比較方便。 您也可以透過 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 的 [選項] 對話方塊執行此作業。  
  
5.  按一下 [安裝]  完成 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 的安裝程序。  
  
## <a name="to-install-ssrbnoversion-from-a-share"></a>從共用安裝[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]  
  
1.  連絡您的系統管理員，取得 ReportBuilder.msi 的執行位置，以在本機電腦上安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]。  
  
2.  瀏覽並找到 ReportBuilder.msi ([!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 的 Windows Installer 套件 (MSI))，然後按一下此檔案。  
  
     隨即啟動 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 精靈。  
  
3.  完成 [若要從下載網站安裝報表產生器](#download)的其餘步驟。  
  
## <a name="to-install-ssrbnoversion-from-the-command-line"></a>若要從命令列安裝 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 

 您也可以執行[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]的命令列安裝，並提供引數來自訂安裝。 除了標準的 MSI 內建參數以外，您還可以使用[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]所提供的自訂參數：RBINSTALLDIR 和 REPORTSERVERURL。 RBINSTALLDIR 會指定[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]的根安裝資料夾。 REPORTSERVERURL 會指定[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]用來在伺服器上儲存報表的預設報表伺服器。  
  
 如果您想要進行完全無訊息的安裝 (完全沒有使用者介面互動)，請指定 **/quiet** 選項。 根據設計，quiet 選項旗標會隱藏安裝錯誤。 因此，當您使用 quiet 選項時，建議您加入 **/l** 選項 (指定記錄)。   
  
1.  在 [Microsoft 下載中心的報表產生器頁面](https://go.microsoft.com/fwlink/?LinkID=734968)，按一下 [下載]  。  
  
2.  完成下載 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 之後，按一下 [儲存]  。  
  
3.  在 **[開始]** 功能表上，按一下 **[執行]** 。  
  
4.  在 [開啟]  方塊中輸入 **cmd.** 。  
  
5.  在 [命令提示字元] 視窗中，巡覽至儲存 ReportBuilder.msi 的資料夾。  
  
6.  輸入下列格式的命令：  
  
     `msiexec/i ReportBuilder.msi /option [value] [/option [value]]`  
  
     安裝[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]的兩個專屬選項是：RBINSTALLDIR 和 REPORTSERVERURL。 您不需要在命令列中包含這些引數。 以下為基準命令：  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  若要執行命令，請按 Enter 鍵。  
  
## <a name="set-ssrbnoversion-defaults"></a>設定[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]預設值  
  
-   安裝[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]之後，您可以設定一些預設選項。 按一下 [檔案]   > [選項]  。  
  
     設定預設 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站或 SharePoint 網站最為實用。 如需詳細資訊，請參閱 [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md)。  
  
-   按一下 [報表產生器]  。  
  
     若您在現有伺服器清單中沒有看到報表伺服器，請關閉 [開啟報表] 對話方塊，然後按一下 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 底部的 [連線]，以連線至伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [啟動報表產生器](../../reporting-services/report-builder/start-report-builder.md)   
 [將報表產生器解除安裝](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
  
