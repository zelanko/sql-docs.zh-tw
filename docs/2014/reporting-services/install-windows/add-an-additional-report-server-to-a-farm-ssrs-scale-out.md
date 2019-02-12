---
title: 將其他報表伺服器新增至伺服器陣列 (SSRS 向外延展) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 03928e651b742061e726b9c92683d9d4e9aebd08
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014829"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>將其他報表伺服器加入至伺服器陣列 (SSRS 向外延展)
  在 SharePoint 伺服器陣列中加入第二個或更多的 SharePoint 模式報表伺服器，可以改善報表伺服器的處理效能和回應時間。 如果您發現新增更多使用者、報表和其他應用程式到報表伺服器時效能降低了，那麼新增額外的報表伺服器可以改善效能。 此外，當硬體發生問題或者您在環境中的個別伺服器上執行一般維護作業時，也建議您加入第二個報表伺服器以提高報表伺服器的可用性。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版開始，在 SharePoint 模式中向外延展 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 環境的步驟會遵循標準 SharePoint 伺服器陣列部署，並且運用 SharePoint 負載平衡功能。  
  
> [!IMPORTANT]  
>  並非所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本都支援向外延展 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 一節[支援的 SQL Server 2014 的版本功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
> [!TIP]  
>  從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版開始，您不會使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來加入伺服器以及向外延展報表伺服器。 SharePoint 產品會在具有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務的 SharePoint 伺服器加入至伺服器陣列時，管理向外延展 Reporting Services。  
  
 如需如何向外延展原生模式報表伺服器的資訊，請參閱[設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。  
  
-   [負載平衡](#bkmk_loadbalancing)  
  
-   [必要條件](#bkmk_prerequisites)  
  
-   [步驟](#bkmk_steps)  
  
-   [其他設定](#bkmk_additional)  
  
##  <a name="bkmk_loadbalancing"></a> 負載平衡  
 除非您的環境具有自訂或協力廠商負載平衡解決方案，否則 SharePoint 將自動管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的負載平衡。 預設的 SharePoint 負載平衡行為是，每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式都將在您已經啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務的所有應用程式伺服器之間取得平衡。 若要確認 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務是否已安裝並啟動，請按一下 SharePoint 管理中心內的 **[管理伺服器上的服務]** 。  
  
##  <a name="bkmk_prerequisites"></a> 必要條件  
  
-   您必須是本機系統管理員，才能執行 SQL Server 安裝程式。  
  
-   電腦必須加入網域。  
  
-   您必須知道裝載 SharePoint 組態和內容資料庫之現有資料庫伺服器的名稱。  
  
-   資料庫伺服器必須設定為允許遠端資料庫連接。  如果不允許，您就無法將新的伺服器加入伺服器陣列，因為新的伺服器將無法建立 SharePoint 組態資料庫的連接。  
  
-   新的伺服器必須安裝目前伺服器陣列伺服器所執行的相同 SharePoint 版本。 例如，如果伺服器陣列已經安裝 SharePoint 2010 Service Pack 1 (SP1)，您也必須在新的伺服器上安裝 SP1，才能讓它加入伺服器陣列。  
  
-   請檢閱下列其他主題，以了解系統與版本需求：  
  
     [在 SharePoint 2010 伺服器陣列中使用 SQL Server BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="bkmk_steps"></a> 步驟  
 本主題中的步驟假設 SharePoint 伺服器陣列管理員要安裝及設定伺服器。 下圖顯示一般三層環境，而且下圖中的編號項目將於下列清單中描述：  
  
-   (1) 多個 Web 前端 (WFE) 伺服器。 WFE 伺服器需要適用於 SharePoint 2010 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。  
  
-   (2) 執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和網站的單一應用程式伺服器，例如管理中心。 下列步驟會將第二個應用程式伺服器加入至這一層。  
  
-   (3) 兩個 SQL Server 資料庫伺服器。  
  
-   (4) 代表軟體或硬體網路負載平衡解決方案 (NLB)。  
  
 ![新增 Reporting Services 應用程式伺服器](../../../2014/sql-server/install/media/rs-sharepointscale.gif "新增 Reporting Services 應用程式伺服器")  
  
 下列步驟假設管理員要安裝及設定伺服器。 此伺服器將在伺服器陣列中設定為新的應用程式伺服器，而且不會當做 Web 前端 (WFE) 使用。  
  
|步驟|說明和連結|  
|----------|--------------------------|  
|執行 SharePoint 2010 產品準備工具|您必須擁有 SharePoint 2010 安裝媒體。 準備工具是安裝媒體上的 **PrerequisiteInstaller.exe** 。|  
|安裝 SharePoint 2010 產品。|1） 選取**伺服器陣列**安裝類型。<br /><br /> 2） 選取**完成**伺服器類型。<br /><br /> 3) 安裝完成時，如果您現有的 SharePoint 伺服器陣列已安裝 SharePoint 2010 SP1，請不要執行 [SharePoint 產品設定精靈]。 您應該先安裝 SharePoint SP1，然後再執行 SharePoint 產品設定精靈。|  
|安裝 SharePoint Server 2010 SP1。|如果您現有的 SharePoint 伺服器陣列已安裝 SharePoint 2010 SP1 下載並安裝從 SharePoint 2010 SP1:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)。<br /><br /> 如需有關 SharePoint 2010 SP1 的詳細資訊，請參閱 [安裝 Office 2010 SP1 和 SharePoint 2010 SP1 時的已知問題](https://support.microsoft.com/kb/2532126)。|  
|執行 SharePoint 產品設定精靈，將伺服器加入至伺服器陣列。|1） 在**Microsoft SharePoint 2010 產品**程式群組中，按一下**Microsoft SharePoint 2010 產品組態精靈**。<br /><br /> 2） 在**連線至伺服器陣列**頁面上，選取**連接到現有的伺服陣列**然後按一下**下一步**。<br /><br /> 3） 在**指定組態資料庫設定**頁面上，輸入用於現有的伺服陣列和組態資料庫的名稱的資料庫伺服器的名稱。 按一下 [下一步] 。<br />**\*\* 重要\* \*** 如果您看到類似下面的錯誤訊息，而且您已經確認自己擁有的權限，然後確認 SQL Server 網路組態，在啟用了哪些通訊協定**Sql ServerConfiguration Manager**: 「 無法連接到資料庫伺服器。 確定資料庫存在、 資料庫是 Sql Server，而且您有適當的權限來存取伺服器。 」<br />**\*\* 重要\* \*** 如果您看到的頁面**伺服器陣列產品及修補狀態**，您必須檢閱頁面上的資訊，然後才可以繼續使用所需的檔案來更新伺服器將伺服器加入至伺服器陣列。<br /><br /> 4） 在**指定的伺服器陣列安全性設定**頁面上輸入您的伺服器陣列複雜密碼，然後按一下**下一步**。 在確認頁面上，按 **[下一步]** 執行精靈。<br /><br /> 5） 按一下**下一步**來執行**伺服陣列組態精靈**。|  
|確認伺服器已加入至 SharePoint 伺服器陣列。|1) 在 SharePoint 管理中心內，按一下 [系統設定] 群組中的 [管理此伺服器陣列中的伺服器]。<br /><br /> 2) 確認已加入新的伺服器，而且狀態正確。<br /><br /> 3） 請注意，您不會看到服務**SQL Server Reporting Services 服務**執行。 下一個步驟將會安裝此服務。<br /><br /> 4） 若要從 WFE 角色中移除此伺服器，請按一下**管理伺服器上的服務**和停止該服務**Microsoft SharePoint Foundation Web 應用程式**。|  
|安裝和設定 Reporting Services SharePoint 模式。|執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝。 如需有關安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式中，請參閱 <<c2> [ 安裝 Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)如果伺服器只會當做應用程式伺服器和伺服器不會使用為一部 wfe 伺服器，您不需要選取**Reporting Services 增益集適用於 SharePoint 產品**上：<br /><br /> **安裝程式角色**頁面上，選取**SQL Server 功能安裝**<br /><br /> **特徵**頁面上，選取**Reporting Services-SharePoint**<br /><br /> -或-<br /><br /> **Reporting Services 組態**頁面上，確認**只安裝**選項選取**Reporting Services SharePoint 模式**。|  
|確認 Reporting Services 可以運作。|1) 在 SharePoint 管理中心內，按一下 [系統設定] 群組中的 [管理此伺服器陣列中的伺服器]。<br /><br /> 2) 確認 [SQL Server Reporting Services 服務] 正在執行。<br /><br /> 如需詳細資訊，請參閱＜ [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)＞|  
  
##  <a name="bkmk_additional"></a> 其他組態  
 您可以將向外延展部署中的個別 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器最佳化為僅執行背景處理，如此伺服器就不會與互動報表執行作業競用資源。 背景處理包括排程、訂閱和資料警示。  
  
 若要變更個別報表伺服器的行為，請將 **RSreportServer.config** 設定檔中的 **\<IsWebServiceEnable>** 設定為 false。  
  
 根據預設，報表伺服器的 \<IsWebServiceEnable> 會設定為 TRUE。 當所有伺服器都設定為 TRUE 時，伺服器陣列中所有節點的互動和背景就能達到負載平衡。  
  
 如果您將所有報表伺服器的 \<IsWebServiceEnable> 設定為 False，當您嘗試使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能時，就會看見類似以下的錯誤訊息：  
  
 未啟用 Reporting Services Web 服務。 設定 Reporting Services SharePoint 服務有至少一個執行個體\<Iswebserviceenable> > 設為 true。 如需詳細資訊，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
## <a name="see-also"></a>另請參閱  
 [將 web 或應用程式的伺服器新增至 SharePoint 2013 中的伺服器陣列](https://technet.microsoft.com/library/cc261752.aspx)   
 [設定服務 (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
