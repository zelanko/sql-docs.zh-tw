---
title: Reporting Services 設定選項（SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.ins.instwizard.reportserverinstoptions.f1
helpviewer_keywords:
- Report Server Installation Options page [SQL Server Installation Wizard]
- report servers [Reporting Services], installing
- SQL Server Installation Wizard, Report Server Installation Options page
ms.assetid: e4561f6c-bc7f-467e-821a-cde8e5cd7391
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 1b54661c47ff40af595be55d444f6c0ffb4bc2cd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952119"
---
# <a name="reporting-services-configuration-options-ssrs"></a>Reporting Services 組態選項 (SSRS)
  您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝精靈的 [Reporting Services 組態]**** 頁面來指定報表伺服器的安裝和設定方式。 某個安裝選項的可用與否，取決於您先前在 [特徵選取]**** 頁面上選擇的選項，以及在安裝報表伺服器時是否也一併安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的本機執行個體。  
  
 在某些情況下，如果安全通訊端層 (SSL) 憑證安裝在電腦上，並繫結至強式萬用字元，則安裝程式將會使用 HTTPS 前置詞建立 Reporting Services URL。 如需如何將憑證對應至 Reporting Services url 的詳細資訊，請參閱設定[安全通訊端層（SSL）連接的報表伺服器](https://go.microsoft.com/fwlink/?LinkId=199089)（https://go.microsoft.com/fwlink/?LinkId=199089)在 SQL Server 線上叢書中。  
  
 如需有關此版本[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]以及安裝和設定的最新資訊，請參閱[其他安裝資訊](https://go.microsoft.com/fwlink/?LinkId=207425)（https://go.microsoft.com/fwlink/?LinkId=207425)。  
  
## <a name="options"></a>選項  
  
### <a name="reporting-services-native-mode"></a>Reporting Services 原生模式  
 如果安裝程式因一項或多項需求不符而無法執行預設報表伺服器組態，安裝精靈可讓您執行最小安裝選項。它會複製您需要的檔案，不過，安裝完成之後，您必須利用 Reporting Services 組態管理員來設定原生模式報表伺服器。  
  
> [!NOTE]  
>  如果您選擇預設安裝選項的其中一個，現有的報表伺服器資料庫檔案會導致安裝失敗。 當您選擇預設安裝選項時，安裝程式會嘗試使用預設名稱來建立報表伺服器資料庫。 如果已有該名稱的資料庫存在，則安裝程式將會失敗，而且您必須回復安裝。 若要避免這個問題，則可在執行安裝程式之前重新命名現有的資料庫，或選擇 [只安裝]**** 選項，讓您可在安裝完成之後指定自訂資料庫設定。  
  
#### <a name="install-and-configure"></a>安裝和設定  
 使用報表伺服器資料庫、服務帳戶和 URL 保留項目的預設值，以原生模式安裝報表伺服器執行個體。 當您選擇這個選項時，安裝完成之後，報表伺服器執行個體便已備妥，隨時可以使用。 安裝程式會利用本機 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體來建立報表伺服器資料庫，並會將報表伺服器設定成使用預設值。  
  
 報表伺服器安裝架構所用的預設值必須對您的系統有效，您才能使用這個選項。 這個選項適合想要在本機安裝所有元件的開發人員以及要試用本軟體的使用者。  
  
 若要檢視有關安裝程式所使用之預設值的資訊，或是要了解無法安裝預設組態的原因，請按一下 [詳細資料]****。 如需原生模式報表伺服器之預設設定的詳細資訊，請參閱[原生模式安裝的預設設定（Reporting Services）](https://go.microsoft.com/fwlink/?LinkId=199091) （https://go.microsoft.com/fwlink/?LinkId=199091)。  
  
#### <a name="install-only"></a>只安裝  
 安裝報表伺服器程式檔、建立報表伺服器服務帳戶，以及註冊報表伺服器 Windows Management Instrumentation (WMI) 提供者。 這個安裝選項稱為「僅限檔案」的安裝。 如果您不想要使用預設組態，請選取這個選項。 如果無法安裝預設組態，或者您正在安裝包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]容錯移轉叢集，這就是唯一可用的選項。 如需僅限檔案安裝的詳細資訊，請參閱[僅限檔案安裝（Reporting Services）](https://go.microsoft.com/fwlink/?LinkId=199093) （https://go.microsoft.com/fwlink/?LinkId=199093)。  
  
 安裝完成之後，您必須建立報表伺服器資料庫以及設定報表伺服器，之後，才能使用它。 若要設定報表伺服器和建立資料庫，請使用 Reporting Services 組態管理員。 如需詳細資訊，請參閱[如何：建立報表伺服器資料庫（Reporting Services 設定）](https://go.microsoft.com/fwlink/?LinkId=199094) （https://go.microsoft.com/fwlink/?LinkId=199094)以及設定[報表伺服器資料庫連接](https://go.microsoft.com/fwlink/?LinkId=199095)（https://go.microsoft.com/fwlink/?LinkId=199095)）。  
  
### <a name="reporting-services-sharepoint-mode"></a>Reporting Services SharePoint 模式  
  
#### <a name="install-only"></a>只安裝  
 安裝報表伺服器程式檔案和 PowerShell 指令程式。 安裝完成之後，您必須啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服務並建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 如需詳細資訊，請參閱下列主題：  
  
-   [安裝 Reporting Services SharePoint 模式報表伺服器，以進行 Power View 和資料警示](https://go.microsoft.com/fwlink/?LinkId=207543)（https://go.microsoft.com/fwlink/?LinkId=207543)。  
  
-   [將 Reporting Services SharePoint 模式安裝為單一伺服器](https://go.microsoft.com/fwlink/?LinkId=207544)陣列（https://go.microsoft.com/fwlink/?LinkId=207544)。  
  
-   [Reporting Services 報表伺服器（SSRS）](https://go.microsoft.com/fwlink/?LinkID=207244) （https://go.microsoft.com/fwlink/?LinkID=207244)。  
  
## <a name="installing-the-reporting-services-add-in-for-sharepoint-technologies"></a>安裝適用於 SharePoint 技術的 Reporting Services 增益集  
 從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本開始，您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈的 [特徵選取] 頁面中，將增益集當做 SQL Server 安裝的一部分來安裝。  
  
 不過，您也可以使用下列其中一種方法來安裝適用於 SharePoint 2010 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集：  
  
-   執行 SharePoint 2010 產品準備工具 **PreRequisiteInstaller.exe**。  
  
-   從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體安裝。 在 **安裝完成之後，按一下** 安裝媒體上 Setup 資料夾中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rsSharePoint.msi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 檔案。  
  
-   下載和安裝增益集。 如需詳細資訊，請參閱[尋找適用于 SharePoint 產品之 Reporting Services 增益集](https://go.microsoft.com/fwlink/?LinkID=208634)的https://go.microsoft.com/fwlink/?LinkID=208634)位置（。  
  
## <a name="see-also"></a>另請參閱  
 [啟動 Reporting Services 組態管理員](https://go.microsoft.com/fwlink/?LinkId=199096)   
 [建立報表伺服器資料庫（Reporting Services 設定）](https://go.microsoft.com/fwlink/?LinkId=199094)   
 [升級和遷移 Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628)   
 [Reporting Services SharePoint 模式和原生模式的命令提示字元安裝](https://go.microsoft.com/fwlink/?LinkId=217620)  
  
  
