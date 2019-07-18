---
title: 升級活頁簿和排程的資料重新整理 (SharePoint 2013) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f0d49d6aeb8231dbffb56b42fe1151ae90d0e41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181305"
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>升級活頁簿和排程的資料重新整理 (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  本主題將說明在先前 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 環境中建立之活頁簿的使用者體驗，以及如何升級 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿，以便讓您運用這個版本所導入的新功能。 若要深入了解新功能，請參閱[What's New in Power Pivot](http://go.microsoft.com/fwlink/?LinkID=203917)。  
  
> [!WARNING]  
>  您不能針對在伺服器上自動升級的活頁簿回復升級。 一旦升級活頁簿之後，它就會保持升級的狀態。 若要使用之前的版本，可以將之前的活頁簿重新發行至 SharePoint、還原之前的版本或回收活頁簿。 如需有關在 SharePoint 中還原或回收文件的詳細資訊，請參閱＜ [規劃如何使用資源回收筒及版本設定功能保護內容](http://go.microsoft.com/fwlink/?LinkId=238669)＞。  
  
  
##  <a name="bkmk_overview"></a> 升級活頁簿的概觀  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿是包含內嵌 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 資料的 Excel 活頁簿。 升級活頁簿有兩個好處：  
  
-   使用 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]中的新功能。  
  
-   針對搭配 SharePoint 模式之 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services 伺服器執行的活頁簿啟用排程的資料重新整理。  
  
> [!IMPORTANT]  
>  您無法回復已升級的活頁簿，所以如果希望在舊版 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]或舊版 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]中使用該活頁簿，請務必製作檔案的複本。  
  
 下表將根據建立活頁簿的環境列出 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿的支援和行為。 描述的行為包括一般使用者體驗、將活頁簿升級為特定環境的支援升級選項，以及尚未升級之活頁簿的排程資料重新整理行為。  
  
### <a name="workbook-behavior-and-upgrade-options"></a>活頁簿行為和升級選項  
  
|建立於|\<|支援和行為|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2010**|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2010**|**2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013**|  
|**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010**|所有功能|**體驗：** 使用者可以與瀏覽器中的活頁簿進行互動，並使用它做為資料來源，為其他方案。<br /><br /> **升級：** 如果已啟用自動升級，活頁簿就會自動升級在文件庫[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]系統中的 SharePoint 伺服陣列的服務<br /><br /> **排程資料重新整理：** 不支援。 活頁簿需要升級。|**體驗：** 使用者可以與活頁簿進行互動，並使用它做為資料來源，為其他方案。<br /><br /> **升級：** 無法使用自動升級。 使用者必須手動將其 2008 R2 活頁簿升級為 2012 版本或 Office 2013 版本。<br /><br /> **排程資料重新整理：** 不支援。 活頁簿需要升級。|  
|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel**|不支援|所有功能|**體驗：** 使用者可以與瀏覽器中的活頁簿進行互動，並使用它做為資料來源，為其他方案。 可以使用排程資料重新整理。<br /><br /> **升級：** 不支援自動升級。 使用者可以手動將其活頁簿升級為 Office 2013 版本。<br /><br /> **排程資料重新整理** ：支援。|  
|**Excel 2013**|不支援|不支援|所有功能|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> 從 2008 R2 活頁簿升級為 SQL Server 2012 Service Pack 1 (SP1) 活頁簿  
 本節將描述如何從 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 活頁簿升級為 SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2013 活頁簿。  
  
 **行為變更：** SQL Server 2008 R2[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]活頁簿不會自動升級用於 SQL Server 2012 SP1 時，[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]適用於 SharePoint 2013。 因此，排程的資料重新整理不會針對 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿運作  
  
 2008 R2 活頁簿將在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 中開啟，但是排程的資料重新整理不會運作。 如果您檢閱重新整理記錄，將會看到類似以下的錯誤訊息：  
  
 「 活頁簿包含不支援[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模型。 活頁簿中的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型是採用 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 格式。 支援的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型如下:  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010。  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2013。  
  
 **如何升級活頁簿：** 之前將活頁簿升級為 2012年活頁簿排程資料重新整理無法運作。 若要升級活頁簿及它所包含的模型，請完成下列其中一項作業：  
  
-   在已安裝 SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 增益集的 Microsoft Excel 2010 中下載並開啟活頁簿。  
  
     開啟 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 視窗，並升級 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型。  
  
     然後，儲存活頁簿並重新發行至 SharePoint。  
  
-   在 Microsoft Excel 2013 中下載並開啟活頁簿。  
  
     開啟 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 視窗，並升級 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型。  
  
     然後，儲存活頁簿並重新發行至 SharePoint 伺服器。  
  
 如需 Analysis Services 功能變更的詳細資訊，請參閱 [SQL Server 2016 中 Analysis Services 功能的行為變更](../../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)  
  
 如需重新整理記錄的詳細資訊，請參閱 [檢視資料重新整理記錄 &#40;Power Pivot for SharePoint&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)(PowerPivot 的新功能)。  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> 從使用 2012 PowerPivot for Excel 增益集所建立的版本升級為 Office 2013 活頁簿  
 本節將描述如何 **從** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 活頁簿升級 **為** SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2013。  
  
 升級活頁簿可解決下列嘗試針對舊版活頁簿進行排程資料重新整理時所發生的錯誤：  
  
 「 重新整理作業用於建立舊版的活頁簿[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]不提供。 」  
  
 **如何升級活頁簿**  
  
1.  在 Microsoft Excel 2013 中手動開啟每個活頁簿，藉以進行升級。  
  
2.  若要升級活頁簿及它所包含的模型，請在 Microsoft Excel 2013 中下載並開啟活頁簿。  
  
3.  開啟 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 視窗，並升級 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型。  
  
4.  然後，儲存活頁簿並重新發行至 SharePoint 2013 伺服器。  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> 從使用 2008 R2 PowerPivot for Excel 2010 增益集所建立的版本升級為 SQL Server 2012 活頁簿  
 本節將描述如何 **從** SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 活頁簿升級 **為** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010。  
  
 升級活頁簿可解決下列嘗試針對舊版活頁簿進行排程資料重新整理時所發生的錯誤：  
  
 「 重新整理作業用於建立舊版的活頁簿[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]不提供。 」  
  
 **如何升級活頁簿**  
  
 升級的方式有兩種：  
  
1.  在具有 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 版 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 的電腦上使用 Excel 來開啟每個活頁簿，藉以手動升級每個活頁簿，然後將它重新發行至伺服器。 當您在新版增益集中開啟活頁簿時，就會執行以下內部作業：活頁簿資料連接字串中的資料提供者會更新為 MSOLAP.5，中繼資料也會更新，而且還會重新建立關聯性，以符合新的實作。  
  
2.  或者，SharePoint 管理員也可以針對 SharePoint 伺服器陣列中的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 系統服務啟用自動升級功能，以便在排程資料重新整理執行時自動升級 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿 (只會升級針對排程資料重新整理設定的活頁簿)。  
  
    > [!NOTE]  
    >  自動升級是伺服器組態功能。您無法針對特定活頁簿、文件庫或網站集合啟用或停用此功能。  
  
 **如何在資料重新整理期間設定自動升級**  
  
 若要使用自動升級，您必須在組態工具中選取 [**自動升級 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿，以便從伺服器進行資料重新整理]** 核取方塊[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]。 在此工具中，該核取方塊位於 [升級 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 系統服務]  頁面上，而且位於 [建立 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式]  頁面上 (如果您要設定新安裝的話)。  
  
 您可以執行下列指令程式來確認是否已啟用自動升級：  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 Get-PowerPivotSystemService 的輸出是屬性和對應值的清單。 您應該會在屬性清單中看見 **WorkbookUpgradeOnDataRefresh** 。 如果自動升級已啟用，它就會設定為 **true** 。 如果它是 **false**，請繼續進行下一個步驟，啟用自動活頁簿升級。  
  
 若要啟用自動活頁簿升級，請執行下列命令：  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true -Confirm:$false  
```  
  
 升級活頁簿之後，您就可以在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 增益集中使用排程的資料重新整理和新功能。  
  
##  <a name="bkmk_runold"></a> 執行較新伺服器上的多個活頁簿版本  
 您可以在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 的 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 執行個體上並存執行舊版與新版的 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]活頁簿。  
  
 根據伺服器的安裝方式而定， **您可能需要** 安裝舊版 Analysis Services OLE DB 提供者，才能在同一部伺服器上存取舊版和新版活頁簿。  
  
 請注意，目前不支援在 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 的舊版 SQL Server 執行個體上發行新版的活頁簿。 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 執行個體無法載入您在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 版 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]中建立的活頁簿，而且 SQL Server 2012 執行個體無法載入包含您使用 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 版 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 所建立之進階資料模型的 Office 2013 活頁簿。  
  
###  <a name="bkmk_msolapxslx"></a> 如何檢查 PowerPivot 活頁簿中的 MSOLAP 資料提供者資訊  
 請使用下列指示，檢查 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿中使用哪一個 OLE DB 提供者。 檢查資料連接資訊不需要安裝 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] 增益集。  
  
1.  在 Excel 中的 [資料] 索引標籤上，按一下 **[連接]** 。 按一下 **[屬性]** 。  
  
2.  在 **[定義]** 索引標籤上，提供者版本會出現在連接字串的開頭。  
  
     []  表示活頁簿為 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
     []  則是指 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。  
  
     []  表示活頁簿是使用內嵌資料庫的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿。  
  
###  <a name="bkmk_msolappc"></a> 如何檢查本機電腦上目前的 MSOLAP 資料提供者版本  
 請使用下列指示，檢查哪一個 OLE DB 提供者是目前在伺服器或工作站上執行 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿的版本。 得知目前版本可協助您在升級之後針對資料連接錯誤進行疑難排解。  
  
1.  在 [登錄編輯器] 中，移至 HKEY_CLASSES_ROOT  
  
2.  向下捲動至 MSOLAP。 確認 MSOLAP.5 列在系統上所安裝的 OLAP 提供者中。 確認 MSOLAP | CurVer 設定為 MSOLAP.5  
  
## <a name="see-also"></a>另請參閱  
 [將 Power Pivot 移轉至 SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [升級 Power Pivot for SharePoint](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Analysis Services 的新功能](../../../analysis-services/what-s-new-in-analysis-services.md)   
 [檢視資料重新整理記錄 &#40;Power Pivot for SharePoint&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
