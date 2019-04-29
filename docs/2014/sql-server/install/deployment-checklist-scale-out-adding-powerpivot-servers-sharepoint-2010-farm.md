---
title: 部署檢查清單：向外延展 PowerPivot 伺服器加入 SharePoint 2010 伺服器陣列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7bef5104038dad251927c6afff613f248f4a6a47
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025696"
---
# <a name="deployment-checklist-scale-out-by-adding-powerpivot-servers-to-a-sharepoint-2010-farm"></a>部署檢查清單：向外延展至 SharePoint 2010 伺服器陣列加入 PowerPivot 伺服器
  如果您預期 SharePoint 伺服器陣列中 PowerPivot 查詢處理有大量的要求，您可以加入額外的 PowerPivot for SharePoint 執行個體，以順暢地新增查詢和資料處理支援。  
  
 安裝新執行個體之後，即會有額外的容量可查詢 PowerPivot 資料或處理 PowerPivot 資料重新整理工作。 或者，您可以選擇設定每部伺服器處理一種要求類型：查詢或資料重新整理。  
  
## <a name="prerequisites"></a>先決條件  
 安裝及設定 SharePoint Server 2010。  
  
 套用 SharePoint Server 2010 SP1 並升級伺服器陣列。  
  
 伺服器陣列中現有的 PowerPivot for SharePoint 執行個體為 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (可以是新安裝或升級自 SQL Server 2008 R2)。  
  
 將您要安裝新 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint 伺服器的電腦加入伺服器陣列。 伺服器陣列中的電腦及其他伺服器必須在同一個網域中。  
  
 請檢閱下列其他主題，以了解系統與版本需求：  
  
-   [在 SharePoint 2010 伺服器陣列中使用 SQL Server BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
> [!NOTE]  
>  在多伺服器的伺服器陣列中，所有 PowerPivot for SharePoint 執行個體都必須是相同的版本。 如果您將 Service Pack 或更新套用到已經在伺服器陣列中的其他 PowerPivot 伺服器，您必須將加入的新執行個體更新為與伺服器陣列中現有執行個體相同的版本。 套用所有更新之後，才可以使用新的執行個體。  
  
## <a name="steps"></a>步驟  
 使用此檢查清單將其他 PowerPivot 伺服器加入至 SharePoint 伺服器陣列。 這些指示假設您已經在伺服器陣列中擁有 PowerPivot for SharePoint 伺服器，而且您要加入第二部伺服器來處理額外的處理負載。 除了安裝需求、後續安裝組態和驗證的差異以外，部署向外延展解決方案的步驟都與將單一 PowerPivot 伺服器加入至現有伺服器陣列相同。  
  
|步驟|連結|  
|----------|----------|  
|判斷已經在伺服器陣列中之 Analysis Services 執行個體的服務帳戶。|您安裝的每個額外執行個體，必須與第一個執行個體在相同的帳戶下執行。 使用任一個方法來判斷此服務帳戶：<br /><br /> 在 [管理中心] 中 [安全性] 區段中，按一下**設定服務帳戶**。 選取  **Windows 服務-SQL Server Analysis Services**。 當您選取此服務之後，服務帳戶名稱將會出現在頁面上。<br /><br /> 在伺服器上已安裝 PowerPivot 服務，開啟**Services**主控台系統管理工具中的應用程式。 按兩下**SQL Server Analysis Services**。 按一下 **登入**索引標籤來檢視服務帳戶。<br />**\*\* 重要\* \*** 只使用管理中心變更服務帳戶。 如果您使用另一個工具或方法，將無法在伺服器陣列中正確更新權限。|  
|執行安裝程式，以安裝第二個 PowerPivot for SharePoint 執行個體。|[安裝 PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> 選擇已加入伺服器陣列、但在伺服器上沒有現有的 PowerPivot 執行個體之應用程式伺服器。<br /><br /> 在安裝期間出現指定服務帳戶的提示時，輸入上一個步驟的帳戶。 Analysis Services 服務的所有執行個體必須在相同的網域帳戶下執行。 此需求會啟用 SharePoint 的受管理帳戶功能，好讓您在一個位置為相同類型的所有服務執行個體更新密碼。|  
|設定第二個執行個體|若要設定執行個體，您可以使用兩種方法：[PowerPivot 組態工具](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)或[使用 Windows PowerShell 的 PowerPivot 組態](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)<br /><br /> 設定第二個執行個體時，您只需要佈建本機服務。 其他所有設定工作 (例如建立服務應用程式或設定資料重新整理) 會在初始組態期間執行，並供您安裝的後續執行個體使用。|  
|後續安裝工作|未具體要求後續的步驟。 您不需要建立服務應用程式、啟動功能、部署方案或是變更服務應用程式識別。 現有的 Web 應用程式和服務應用程式將會自動探索及使用新的伺服器軟體。<br /><br /> 或者，如果您安裝第二部伺服器的目的，是為了讓其中一部伺服器用於查詢，而另一部伺服器用於資料重新整理，您可以立即設定伺服器執行個體屬性，以指定每部伺服器處理的要求類型。 如需詳細資訊，請參閱 < [Configure Dedicated Data Refresh or Query-Only &#40;PowerPivot for SharePoint&#41;](../../analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)。|  
|確認第二個執行個體的安裝|您可以使用下列步驟，在您剛才安裝的伺服器上驗證 PowerPivot 查詢處理。<br /><br /> 1） 在 管理中心 中，開啟管理伺服器 頁面來確認伺服器和其服務出現上的服務。<br />-在伺服器中，按一下向下箭號，按一下 變更伺服器，然後選取已安裝全新 PowerPivot for SharePoint 的伺服器。<br />-確認 SQL Server Analysis Services 和 SQL Server PowerPivot 系統服務都已啟動。<br /><br /> 2） 在 管理中心 的 停止其他 PowerPivot for SharePoint 伺服器，讓您剛才安裝的伺服器是唯一可用的。 如需詳細資訊，請參閱 <<c0> [ 啟動或停止 PowerPivot for SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)。<br /><br /> 3） 按一下以開啟從程式庫的 PowerPivot 活頁簿。<br /><br /> 4） 按一下交叉分析篩選器，或起始查詢針對資料執行樞紐。 伺服器將會在背景載入 PowerPivot 資料。 在下一個步驟中，您將會連接到伺服器，並確認已經載入及快取資料。<br /><br /> 5） 從 [開始] 功能表中的 Microsoft SQL Server 程式群組啟動 SQL Server Management Studio。 如果伺服器上未安裝這個工具，您可以跳到最後一個步驟，確認快取檔案存在。<br /><br /> 6） 在 伺服器類型，選取**Analysis Services**。<br /><br /> 7） 在 伺服器名稱，輸入**\<伺服器名稱 > \powerpivot**，其中**\<伺服器名稱 >** 是已安裝全新 PowerPivot for SharePoint 的電腦名稱。<br /><br /> 8） 按一下**連線**。<br /><br /> 9） 在 [物件總管] 中，按一下**資料庫**，檢視載入的 PowerPivot 資料檔案的清單。<br /><br /> 10） 上的電腦檔案系統中，請檢查下列資料夾來判斷檔案是否要快取到磁碟。 快取檔案的存在會進一步驗證您的部署是否可以運作。 若要檢視檔案快取，請移至 \Program Files\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup 資料夾。<br /><br /> 11） 重新啟動您稍早停止的服務。|  
  
## <a name="see-also"></a>另請參閱  
 [初始設定&#40;PowerPivot for SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [管理中心的 PowerPivot 伺服器管理和設定](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
