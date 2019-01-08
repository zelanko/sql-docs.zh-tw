---
title: 行為變更 Analysis Services SQL Server 2014 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0f7cc154a79a329bc18d02535e3f3332aa7e8b61
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391781"
---
# <a name="behavior-changes-to-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 中 Analysis Services 功能的行為變更
  本主題描述 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中多維度、表格式、資料採礦及 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 部署的行為變更。 行為變更會影響功能在目前版本中，與舊版 SQL Server 相較之下的運作或互動方式。  
  
> [!NOTE]  
>  相反地，中斷變更則防止已與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 整合的資料模型或應用程式執行。 如需詳細資訊，請參閱＜ [Breaking Changes to Analysis Services Features in SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)＞。  
  
 本主題內容：  
  
-   [SQL Server 2014 中的行為變更](#bkmk_sql2014)  
  
-   [SQL Server 2012 SP1 中的行為變更](#bkmk_sql2012sp1)  
  
-   [SQL Server 2012 中的行為變更](#bkmk_sql2012)  
  
##  <a name="bkmk_sql2014"></a> 中的行為變更 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 此版本中的多維度、表格式、資料採礦或 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 功能皆未宣告任何新的行為變更。  不過，因為  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 很類似 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 版本，所以在此為您提供這兩個舊版的行為變更，以便您從 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]升級。  
  
##  <a name="bkmk_sql2012sp1"></a> 中的行為變更 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]  
 本章節記載針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]功能所報告的行為變更。 這些變更也適用於 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]。  
  
|問題|描述|  
|-----------|-----------------|  
|在 SQL Server 2012 SP1 PowerPivot for SharePoint 2013 中使用 SQL Server 2008 R2 PowerPivot 活頁簿時，這些活頁簿不會以無訊息方式升級並重新整理模型。 因此，排程的資料重新整理不會針對 SQL Server 2008 R2 PowerPivot 活頁簿運作。|2008 R2 活頁簿將在 [!INCLUDE[ssGeminiShortvnext](../includes/ssgeminishortvnext-md.md)]中開啟，但是排程的重新整理不會運作。 如果您檢閱重新整理記錄，將會看到類似以下的錯誤訊息：<br /> 「 活頁簿包含不支援的 PowerPivot 模型。 活頁簿中的 PowerPivot 模型是採用 SQL Server 2008 R2 PowerPivot for Excel 2010 格式。 支援的 PowerPivot 模型如下: <br />SQL Server 2012 PowerPivot for Excel 2010<br />SQL Server 2012 PowerPivot for Excel 2013 」<br /><br /> **如何升級活頁簿：** 在您將活頁簿升級為 2012 活頁簿之前，排程的重新整理無法運作。 若要升級活頁簿及它所包含的模型，請完成下列其中一項作業：<br /><br /> 在已安裝 SQL Server 2012 PowerPivot for Excel 增益集的 Microsoft Excel 2010 中下載並開啟活頁簿。 然後，儲存活頁簿並重新發行至 SharePoint 伺服器。<br /><br /> 在 Microsoft Excel 2013 中下載並開啟活頁簿。 然後，儲存活頁簿並重新發行至 SharePoint 伺服器。<br /><br /> <br /><br /> 如需有關活頁簿升級的詳細資訊，請參閱 <<c0> [ 升級活頁簿和排程資料重新整理&#40;SharePoint 2013&#41;](instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。</c0>|  
|DAX [ALL Function](https://msdn.microsoft.com/library/ee634802(v=sql.120).aspx)中的行為變更。|在 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]之前，如果您將標示的 [日期] 資料行指定為日期資料表以供時間智慧使用，則該 [日期] 資料行會傳遞為 ALL 函數的引數，接著會傳遞為 CALCULATE 函數的篩選條件，並且資料表中所有資料行的所有篩選條件都會被忽略，不論日期資料行上是否使用任何交叉分析篩選器。<br /><br /> 例如，<br /><br /> `= CALCULATE (<expression>, ALL (DateTable[Date]))`<br /><br /> 在 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]之前，日期資料表的所有資料行都會忽略所有篩選條件，不論 [日期] 資料行是否當做 ALL 的引數傳遞。<br /><br /> 在 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 和 Excel 2013 的 PowerPivot 中，此行為只會忽略當做 ALL 的引數傳遞之指定資料行的篩選條件。<br /><br /> 若要避開新的行為，事實上是忽略當做整個資料表之篩選條件的所有資料行，您可以從引數中排除 [日期] 資料行，例如，<br /><br /> `=CALCULATE (<expression>, ALL(DateTable))`<br /><br /> 這樣會產生與之前 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]相同的行為結果。|  
  
##  <a name="bkmk_sql2012"></a> 中的行為變更 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 本章節記載針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能所報告的重大變更。 這些變更也適用於 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]。  
  
### <a name="analysis-services-multidimensional-mode"></a>Analysis Services 多維度模式  
  
#### <a name="nullprocessing-option-set-to-preserve-is-no-longer-supported-for-distinct-count-measures"></a>相異計數量值不再支援將 NullProcessing 選項設為 Preserve  
 之前[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]，即可設定[NullProcessing 元素&#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl)來`Preserve`相異計數量值。  不幸的是，這種做法產生的結果時常無效，有時甚至會損毀正在處理的作業。 因此 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]將不再提供這項設定。 嘗試使用它將會導致下列驗證錯誤發生：「 中繼資料管理員中的錯誤。 Preserve 不是有效 NullProcessing 值\<measurename > 相異計數量值。 」  
  
#### <a name="cube-browser-in-management-studio-and-cube-designer-has-been-removed"></a>已經移除 Management Studio 和 Cube 設計師中的 Cube 瀏覽器  
 已經從產品中移除 Cube 瀏覽器控制項，此控制項可讓您將欄位拖放到 Management Studio 或 Cube 設計師中的樞紐分析表結構上。 此控制項為 Office Web 控制項 (OWC) 元件。 OWC 已被 Office 取代，無法再使用。  
  
### <a name="powerpivot-for-sharepoint"></a>PowerPivot for SharePoint  
  
#### <a name="higher-permission-requirements-for-using-a-powerpivot-workbook-as-an-external-data-source"></a>使用做為外部資料來源的 PowerPivot 活頁簿需要更高的權限  
 Excel 活頁簿可以轉譯相同活頁簿中內嵌的 PowerPivot 資料，或是外部活頁簿中的 PowerPivot 資料。 在舊版中，無論是內嵌的還是外部的 PowerPivot 資料，權限要求都相同。 如果您擁有 PowerPivot 活頁簿的 **[僅檢視]** 權限，就能夠同時針對內嵌和外部連接，完整存取活頁簿中的所有 PowerPivot 資料。  
  
 在此版本中，從外部檔案轉譯 PowerPivot 資料之 Excel 活頁簿的權限要求已變更。 在此版本中，您必須擁有 **[讀取]** 權限 (更具體來說，就是 **[開啟項目]** 權限)，才能從用戶端應用程式連接到外部的 PowerPivot 活頁簿。 額外的權限會指定使用者具備下載權限才能檢視活頁簿中內嵌的來源資料。 其他權限會反映模型資料完全可用於所連結的用戶端應用程式或活頁簿，導致在權限要求與實際資料連接行為之間獲得更好的協調。  
  
 若要繼續使用 PowerPivot 活頁簿做為外部資料來源，您必須為連接到外部 PowerPivot 資料的使用者建立 SharePoint 權限。 除非您變更權限，否則使用者嘗試在資料來源連接中存取 PowerPivot 活頁簿時會收到下列錯誤：「 PowerPivot Web 服務傳回錯誤 （拒絕存取。 您所要求的文件不存在或您沒有開啟檔案的權限。） 」  
  
> [!WARNING]  
>  以下步驟說明如何在文件庫層級中斷權限繼承，並且將使用者對此文件庫中特定文件的權限從 **[僅檢視]** 提升為 **[讀取]** 。 在繼續進行之前，務必仔細檢越現有權限和文件，並且確認這些步驟適合您的網站。  
>   
>  或者，您可以在文件庫中建立資料夾，將所有受影響的文件移到該資料夾中，然後在資料夾上設定唯一的權限。  
  
> [!NOTE]  
>  如果您的活頁簿存放在 PowerPivot 圖庫中，中斷活頁簿的權限繼承將會使活頁簿的縮圖影像無法產生 (如果已設定活頁簿進行資料重新整理的話)。 若要同時允許存取圖庫中的活頁簿和預覽影像，請考慮在文件庫層級將文件庫中所有文件的 **[讀取]** 權限授與特定使用者。  
  
 您必須是網站擁有者，才能變更權限。  
  
 **如何增加讀取個別活頁簿的權限層級的權限**  
  
1.  按一下向下箭號，開啟個別文件的功能表。  
  
2.  按一下 **[管理權限]**。  
  
3.  根據預設，文件庫會繼承權限。 若要變更此文件庫中個別活頁簿的權限，按一下 **[停止繼承權限]**。  
  
4.  依使用者或群組名稱，選取需要 PowerPivot 活頁簿其他權限的核取方塊。 其他權限將允許這些使用者連結到內嵌的 PowerPivot 資料，並使用該資料做為其他文件中的外部資料來源。  
  
5.  按一下 **[編輯使用者權限]**。  
  
6.  選擇 **[讀取]** 權限，然後按一下 **[確定]**。  
  
#### <a name="powerpivot-gallery-new-rules-for-snapshot-generation-for-some-powerpivot-workbooks"></a>PowerPivot 圖庫：針對部分 PowerPivot 活頁簿產生快照的新規則  
 此版本導入了在 PowerPivot 圖庫中產生快照影像的新需求，以避免可能洩漏資訊來源 (也就是從您沒有檢視權限的資料來源顯示資料的快照)。 這些需求僅適用於每次檢視活頁簿時連接到外部資料來源的 PowerPivot 活頁簿。 如果您只有使用視覺化內嵌 PowerPivot 資料的活頁簿，就不會看見在 PowerPivot 圖庫中產生快照之方式的改變。  
  
 針對每次開啟都會重新整理其資料的活頁簿，產生快照的新需求如下：  
  
-   其他活頁簿或報表用來做為外部資料來源的 PowerPivot 活頁簿，必須與取用資料的活頁簿位於相同的文件庫中。 例如，如果您有提供資料給 sales-report.xlsx 的 sales-data.xlsx，則這兩個活頁簿必須都在圖庫中，快照影像才會出現。  
  
-   搭配使用的活頁簿必須從共同的父系繼承權限 (也就是 PowerPivot 圖庫)。 在上述範例中，sales-data.xlsx 和 sales-report.xlsx 都必須從 PowerPivot 圖庫繼承。  
  
 如果活頁簿未能符合上述任何準則，則會出現下列鎖定圖示，而不會顯示您要的縮圖影像：  
  
 ![GMNI_PowerPivotGalleryIcon_Locked](media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")  
  
#### <a name="new-default-setting-for-load-balancing-requests-changed-from-round-robin-to-health-based"></a>負載平衡要求的新預設設定從「循環配置資源」變更為「依據健全狀態」  
 PowerPivot 服務應用程式的預設設定會決定如何將 PowerPivot 資料的要求分散至伺服陣列中的多部 PowerPivot for SharePoint 伺服器。 在舊版中，預設設定為 **[循環配置資源]**，這項設定會在可用的伺服器之間循序分散要求。 而在此版本中，預設現在為 **[依據健全狀態]**。 PowerPivot 服務應用程式會使用伺服器健全狀況統計資料 (例如可用的記憶體或 CPU)，決定哪個伺服器執行個體取得 xt 要求。  
  
 如果您已從舊版升級伺服器，PowerPivot 服務應用程式仍會保留舊的預設設定 (**[循環配置資源]**)。 若要使用 **[依據健全狀態]** 配置方法設定，則必須修改組態設定。 如需詳細資訊，請參閱 [建立及設定 PowerPivot 服務應用程式](power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)。  
  
## <a name="see-also"></a>另請參閱  
 [回溯相容性](../../2014/getting-started/backward-compatibility.md)   
 [重大變更 Analysis Services SQL Server 2014 中的功能](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
  
