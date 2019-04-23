---
title: 將其他 Reporting Services Web 前端新增至伺服器陣列 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b2bd5c489bf799e39b51bf61f0f9e8922a993f65
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947554"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>將其他 Reporting Services Web 前端加入至伺服器陣列
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式包含應用程式伺服器和 Web 前端 (WFE) 伺服器所需的元件。 本主題的重點在於安裝 WFE 伺服器的必要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能所使用的應用程式頁面，例如訂閱、資料警示和 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。 WFE 所需的主要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝是安裝適用於 SharePoint 2010 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。  
  
## <a name="prerequisites"></a>先決條件  
  
-   您必須是本機系統管理員，才能執行 SQL Server 安裝程式。  
  
-   電腦必須加入網域。  
  
-   您必須知道裝載 SharePoint 組態和內容資料庫之現有資料庫伺服器的名稱。  
  
-   資料庫伺服器必須設定為允許遠端資料庫連接。  如果不允許，您就無法將新的伺服器加入伺服器陣列，因為新的伺服器將無法建立 SharePoint 組態資料庫的連接。  
  
-   新的伺服器必須安裝目前伺服器陣列伺服器所執行的相同 SharePoint 版本。 例如，如果伺服器陣列已經安裝 SharePoint 2010 Service Pack 1 (SP1)，您也必須在新的伺服器上安裝 SP1，才能讓它加入伺服器陣列。  
  
-   請檢閱下列其他主題，以了解系統與版本需求：  
  
     [在 SharePoint 2010 伺服器陣列中使用 SQL Server BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>步驟  
 本主題中的步驟假設 SharePoint 伺服器陣列管理員要安裝及設定伺服器。 下圖顯示一般三層環境，而且下圖中的編號項目將於下列清單中描述：  
  
-   (1) 多個 Web 前端 (WFE) 伺服器。 WFE 伺服器需要適用於 SharePoint 2010 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。 下列步驟會將第二個應用程式伺服器加入至這一層。  
  
-   (2) 執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和網站的兩個應用程式伺服器，例如管理中心。  
  
-   (3) 兩個 SQL Server 資料庫伺服器。  
  
-   (4) 代表軟體或硬體網路負載平衡解決方案 (NLB)。  
  
 ![將 SSRS 新增至新的 SharePoint WFE](../../../2014/sql-server/install/media/rs-sharepointscale-wfe.gif "將 SSRS 新增至新的 SharePoint WFE")  
  
 下列步驟假設管理員要安裝及設定伺服器。  
  
|步驟|說明和連結|  
|----------|--------------------------|  
|執行 SharePoint 2010 產品準備工具|您必須擁有 SharePoint 2010 安裝媒體。 準備工具是安裝媒體上的 **PrerequisiteInstaller.exe** 。|  
|安裝 SharePoint 2010 產品。|1） 選取**伺服器陣列**安裝類型。<br /><br /> 2） 選取**完成**伺服器類型。<br /><br /> 3) 安裝完成時，如果您現有的 SharePoint 伺服器陣列已安裝 SharePoint 2010 SP1，請不要執行 [SharePoint 產品設定精靈]。 您應該先安裝 SharePoint SP1，然後再執行 SharePoint 產品設定精靈。|  
|安裝 SharePoint Server 2010 SP1。|如果您現有的 SharePoint 伺服器陣列已安裝 SharePoint 2010 SP1 下載並安裝從 SharePoint 2010 SP1:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)。<br /><br /> 如需有關 SharePoint 2010 SP1 的詳細資訊，請參閱 [安裝 Office 2010 SP1 和 SharePoint 2010 SP1 時的已知問題](https://support.microsoft.com/kb/2532126)。|  
|執行 SharePoint 產品設定精靈，將伺服器加入至伺服器陣列。|1） 在**Microsoft SharePoint 2010 產品**程式群組中，按一下**Microsoft SharePoint 2010 產品組態精靈**。<br /><br /> 2） 在**連線至伺服器陣列**頁面上，選取**連接到現有的伺服陣列**然後按一下**下一步**。<br /><br /> 3） 在**指定組態資料庫設定**頁面上，輸入用於現有的伺服陣列和組態資料庫的名稱的資料庫伺服器的名稱。 按一下 [下一步] 。<br />**&#42;&#42;重要&#42; &#42;** 如果您看到類似下面的錯誤訊息，而且您已經確認自己擁有的權限，然後確認 SQL Server 網路組態，在啟用了哪些通訊協定**Sql ServerConfiguration Manager**。 「 無法連接到資料庫伺服器。 確定資料庫存在、 資料庫是 Sql Server，而且您有適當的權限來存取伺服器。 」<br />**&#42;&#42;重要&#42; &#42;** 如果您看到的頁面**伺服器陣列產品及修補狀態**，您必須檢閱頁面上的資訊，並使用所需的檔案更新伺服器，您可以繼續將加入伺服陣列伺服器。<br /><br /> 4） 在**指定的伺服器陣列安全性設定**頁面上輸入您的伺服器陣列複雜密碼，然後按一下**下一步**。 在確認頁面上，按 **[下一步]** 執行精靈。<br /><br /> 5） 按一下**下一步**來執行**伺服陣列組態精靈**。|  
|確認伺服器已加入至 SharePoint 伺服器陣列。|1) 在 SharePoint 管理中心內，按一下 [系統設定] 群組中的 [管理此伺服器陣列中的伺服器]。<br /><br /> 2) 確認已加入新的伺服器，而且狀態正確。<br /><br /> 3） 若要從 WFE 角色中移除此伺服器，請按一下**管理伺服器上的服務**和停止該服務**Microsoft SharePoint Foundation Web 應用程式**。|  
|安裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]增益集適用於 SharePoint 2010 產品。|安裝此增益集的方法有許多種。 下列步驟會使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝精靈。 如需有關安裝增益集的詳細資訊，請參閱 <<c0> [ 安裝或解除安裝 Reporting Services 增益集 for SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。</c0> 執行[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安裝：<br /><br /> 1) 在 [安裝程式角色] 頁面上，選取 [SQL Server 功能安裝]<br /><br /> 2） 在**特徵**頁面上，選取**Reporting Services 增益集適用於 SharePoint 產品**<br /><br /> 3） 按一下**下一步**在後續許多頁面，並完成安裝選項上。<br /><br /> 如需有關安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，請參閱[安裝 Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|確認新的伺服器可以運作。|1) 在 SharePoint 管理中心內，按一下 [系統設定] 群組中的 [管理此伺服器陣列中的伺服器]。<br /><br /> 2) 確認新的伺服器位於清單中。|  
|更新您的 NLB 解決方案。|依照適當的情況，將您的硬體或軟體 NLB 環境更新為包含新的伺服器。|  
  
## <a name="see-also"></a>另請參閱  
 [新增網頁或應用程式伺服器至伺服器陣列 (SharePoint Server 2010)](https://technet.microsoft.com/library/bb218968.aspx?missingurl=%2fen-us%2flibrary%2fe1aeaddf-6ee4-43a9-82b7-db20b68c71db\(Office.14\))   
 [設定服務 (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
