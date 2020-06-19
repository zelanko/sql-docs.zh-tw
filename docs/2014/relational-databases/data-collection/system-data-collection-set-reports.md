---
title: 系統資料收集組報表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d7f7af7d70cb136b530cfb761cb402ecf0dc6b58
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970408"
---
# <a name="system-data-collection-set-reports"></a>系統資料收集組報表
  資料收集器會針對每個系統資料收集組提供歷程記錄報表。 下列每份報表都會使用儲存在管理資料倉儲中的資料：  
  
-   [磁碟使用量摘要](#Disk)  
  
-   [查詢統計資料記錄](#Query)  
  
-   [伺服器活動記錄](#Server)  
  
 您可以使用這些報表來取得監視系統容量和疑難排解系統效能的資訊。  
  
##  <a name="disk-usage-summary-report"></a><a name="Disk"></a> 磁碟使用量摘要報表  
 [磁碟使用量摘要] 報表包含有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中所有資料庫之磁碟空間使用量的資料。 這些報表中提供的資料是使用 [磁碟使用量] 收集組所取得，而此收集組會使用一般 T-SQL 查詢收集器類型。  
  
 您可以從 [物件總管] 中存取 [磁碟使用量摘要] 報表。 若要檢視此報表，請展開 [管理]  資料夾、以滑鼠右鍵按一下 [資料收集]  、依序指向 [報表]  和 [管理資料倉儲]  ，然後按一下 [磁碟使用量摘要]  。 如需詳細資訊，請參閱 [檢視收集組報表 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)執行個體中所有資料庫之磁碟空間使用量的資料。  
  
### <a name="disk-usage-collection-set-report"></a>磁碟使用量收集組報表  
 [磁碟使用量收集組] 報表會提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中所有資料庫所使用之磁碟空間的概觀，以及每個資料庫之資料和記錄檔的成長趨勢。  
  
-   摘要資料表會顯示資料收集器正在監視之伺服器上已安裝之所有資料庫的開始大小 (以 MB 為單位) 和目前大小。  
  
-   資料和記錄檔的趨勢和平均成長資訊會以圖形方式和數值方式顯示。  
  
#### <a name="disk-usage-collection-set---database-database_name-subreport"></a>磁碟使用量收集組 - 資料庫: <database_name> 子報表  
 當您在 [磁碟使用量收集組] 報表的摘要資料表中按一下特定資料庫或記錄檔的趨勢線時，就會顯示 [磁碟使用量收集組 - 資料庫: <資料庫名稱>  ] 子報表。 這份報表會提供在報告期間內磁碟空間使用量中成長趨勢的圖形表示。 磁碟使用量會依據資料檔的使用空間、資料空間、未配置空間和索引空間以及記錄檔的使用空間和未使用空間進行組織和報告。  
  
 圖表下方的資料表會列出資料收集時間和對應的使用量資料。  
  
#### <a name="disk-usage-for-database-database_name-subreport"></a>資料庫的磁碟使用量: <database_name> 子報表  
 當您在 [磁碟使用量收集組] 報表的摘要資料表中按一下資料庫名稱時，就會顯示 [資料庫的磁碟使用量: <資料庫名稱>]   子報表。 這份報表會提供資料庫資料和交易記錄檔之空間使用量的數值與圖形細目。 資料檔的空間使用量會分類成配置給索引頁面、未配置空間、資料頁面和未使用空間的百分比。 這些類別目錄的定義方式如下：  
  
|類別|定義|  
|--------------|----------------|  
|索引|用來保存索引頁面的磁碟空間量。|  
|未配置|可供資料庫使用但尚未配置給任何物件的磁碟空間量。|  
|資料|資料頁面所使用的磁碟空間量。|  
|未使用|配置給一個或多個物件但尚未使用的磁碟空間量。|  
  
 交易記錄檔的空間使用量會分類成使用空間和未使用空間。  
  
 如果已經在資料庫中發生自動成長和自動壓縮事件，就會針對資料和記錄檔報表這些事件。 此報表會顯示每個事件的開始時間和持續時間以及產生的檔案大小變更。  
  
 系統會報告資料庫中每個資料檔所使用的磁碟空間。 報告成 [保留的空間] 的空間是指使用的空間量加上配置給檔案但尚未使用的空間量。 [使用的空間] 所報告的空間是指檔案目前使用的實際空間，但不包含配置的空間。  
  
##  <a name="query-statistics-history-report"></a><a name="Query"></a> 查詢統計資料記錄報表  
 [查詢統計資料記錄] 報表包含查詢執行統計資料。 這份報表所使用的資料是使用 [查詢統計資料] 收集組取得的，而此收集組會使用查詢活動收集器類型。  
  
 您可以從 [物件總管] 中存取 [查詢統計資料記錄] 報表。 若要檢視此報表，請展開 [管理]  資料夾、以滑鼠右鍵按一下 [資料收集]  、依序指向 [報表]  和 [管理資料倉儲]  ，然後按一下 [查詢統計資料記錄]  。 如需詳細資訊，請參閱 [檢視收集組報表 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)執行個體中所有資料庫之磁碟空間使用量的資料。  
  
### <a name="selecting-data-to-include-in-the-report"></a>選取要包含在此報表中的資料  
 此報表包含整個資料收集週期的查詢執行統計資料。 有兩種方式可讓您逐一導覽資料收集時間表，以便選取要檢視的資料區段。  
  
 **時間表控制項和導覽按鈕**  
  
 您可以使用時間表控制項和導覽按鈕，在時間表中移動或選取日期範圍。 箭頭按鈕會提供向左和向右捲動功能，所以您可以在時間表中前後移動。 根據預設，箭頭會以 4 小時的遞增在時間表中移動。 您可以使用放大鏡按鈕，將這個時間遞增放大或縮小成下列其中一個值：15 分鐘、1 小時、4 小時、12 小時或 24 小時。 目前選取的時間範圍是以反白顯示的時間表部分表示，並且顯示在時間表下方的文字中。 每當您按一下時間表或使用導覽按鈕時，就會更新這些值以及報表中的資料。  
  
 **行事曆按鈕**  
  
 您可以使用行事曆按鈕來指定您要報告之資料的開始日期、開始時間以及持續時間。  
  
#### <a name="query-statistics-history-report"></a>查詢統計資料記錄報表  
 [依總 CPU 排名最前的查詢] 圖表會根據總 CPU 使用量，針對選取的時間範圍顯示每個查詢的相對成本。 若要顯示相對查詢成本的不同檢視，請按一下圖表下面所提供的其中一個超連結：[持續時間]  、[總 I/O]  、[實體讀取]  或 [邏輯寫入]  。  
  
 位於圖表下方的資料表會提供其他查詢資料。 它會列出每個圖表化查詢的文字，以及詳細的統計資訊。 請注意，圖表列與資料表中所示的每個查詢都是作用中連結。 按一下作用中連結就會開啟查詢的 [查詢詳細資料] 子報表。  
  
#### <a name="query-details-subreport"></a>查詢詳細資料子報表  
 [查詢詳細資料] 子報表會提供整個查詢文字。 查詢旁邊有一個 **[編輯查詢文字]** 超連結。 您可以按一下此連結，以便在查詢編輯器中開啟查詢。 查詢下方的資料表會提供查詢執行統計資料，例如每個查詢執行的平均持續時間。  
  
 此時會顯示查詢計畫和每個執行之平均持續時間的圖表。 若要顯示相對查詢計畫成本的不同檢視，請按一下圖表下面所顯示的任何一個超連結： **[持續時間]** 、 **[實體讀取]** 或 **[邏輯寫入]** 。 其圖表線條處於作用中狀態，而且您可以按一下任何一點，以便開啟 [查詢計畫詳細資料] 子報表。  
  
 圖表下方的資料表會根據每次執行的 CPU 使用量顯示前 10 個查詢計畫。 [計劃號碼]  資料行中的每個號碼都是作用中連結，而且您可以按一下此連結，以便開啟 [查詢計劃詳細資料] 子報表。  
  
#### <a name="query-plan-details-subreport"></a>查詢計畫詳細資料子報表  
 這份報表會顯示查詢計畫的資訊。 除了讓您編輯查詢和檢視執行統計資料以外，此報表還會提供有關查詢計畫的詳細資訊。 **[檢視圖形的查詢執行計畫]** 超連結會針對目前的查詢開啟執行計畫的圖形表示。  
  
## <a name="server-activity-history-report"></a>伺服器活動記錄報表  
 [伺服器活動記錄] 報表包含伺服器與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的資源耗用量和伺服器活動資料。 這份報表中提供的資料是由 [伺服器活動] 收集組所收集的，而此收集組會使用一般 T-SQL 查詢收集器類型和效能計數器收集器類型。  
  
 您可以從 [物件總管] 中存取 [伺服器活動記錄] 報表。 若要檢視此報表，請展開 [管理]  資料夾、以滑鼠右鍵按一下 [資料收集]  、依序指向 [報表]  和 [管理資料倉儲]  ，然後按一下 [伺服器活動記錄]  。 如需詳細資訊，請參閱 [檢視收集組報表 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)執行個體中所有資料庫之磁碟空間使用量的資料。  
  
### <a name="selecting-data-to-include-in-the-report"></a>選取要包含在此報表中的資料  
 此報表包含整個資料收集週期的伺服器活動。 有兩種方式可讓您逐一導覽資料收集時間表，以便選取要檢視的資料區段。  
  
 **時間表控制項和導覽按鈕**  
  
 您可以使用時間表控制項和導覽按鈕，在時間表中移動或選取日期範圍。 箭頭按鈕會提供向左和向右捲動功能，所以您可以在時間表中前後移動。 根據預設，箭頭會以 4 小時的遞增在時間表中移動。 您可以使用放大鏡按鈕，將這個時間遞增放大或縮小成下列其中一個值：15 分鐘、1 小時、4 小時、12 小時或 24 小時。 目前選取的時間範圍是以反白顯示的時間表部分表示，並且顯示在時間表下方的文字中。 每當您按一下時間表或使用導覽按鈕時，就會更新這些值以及報表中的資料。  
  
 **行事曆按鈕**  
  
 您可以使用行事曆按鈕來指定您要報告之資料的開始日期、開始時間以及持續時間。  
  
###  <a name="server-activity-history-report"></a><a name="Server"></a> 伺服器活動記錄報表  
 [伺服器活動記錄] 報表會顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體與主機作業系統之伺服器活動的初始檢視。  
  
 下表描述的是繪製報表中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與系統活動的圖表，以及可透過這些圖表存取的詳細子報表。  
  
|圖形|報表描述|  
|-----------|------------------------|  
|%CPU|您可以在 %CPU 圖表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或系統圖表線條上按一下任何一點，即可存取這些子報表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> [查詢統計資料記錄] 報表會提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中成本最高之查詢的圖表。 此圖表下方的資料表會列出這些查詢並且包含每個查詢的統計資料。 您可以按一下查詢，以便取得其他詳細資料。<br /><br /> 系統<br /> [系統 CPU 使用量] 報表會提供每個處理器之 %CPU 時間的圖表，並且以表格式格式提供每個處理序的統計資料。|  
|記憶體使用量|您可以在記憶體使用量圖表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或系統圖表線條上按一下任何一點，即可存取這些子報表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體使用量] 報表會提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序記憶體使用量、記憶體計數器和內部記憶體耗用量 (依據類型) 的圖表，以及提供平均記憶體使用量 (依據元件類型) 之相關資訊的資料表。<br /><br /> 系統<br /> [系統記憶體使用量] 報表會提供記憶體使用量、快取和頁面叫用比率的圖表，以及提供每個處理序之工作集和私用位元組的相關資訊的資料表。|  
|磁碟 I/O 使用量|您可以在磁碟 I/O 使用量圖表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或系統圖表線條上按一下任何一點，即可存取這些子報表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 使用量] 報表會提供磁碟回應時間和磁碟傳輸率的圖表。 有一份額外的資料表會依據磁碟、資料庫和檔案來提供虛擬檔案統計資料。<br /><br /> 系統<br /> [系統磁碟使用量] 報表會提供磁碟回應時間、平均磁碟佇列長度和磁碟傳輸率的圖表，以及提供每個處理序之 IO 寫入與讀取的相關資訊的資料表。|  
|網路使用量|沒有其他報表可用。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等候|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等候圖表會顯示等候類別所執行之執行緒所遇到的等候。 您可以按一下圖表中的任何區段，藉以存取詳細的報表。 除了針對一段縮短的時間範圍提供圖形 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等候統計資料以外，這份報表還會以表格式格式提供等候類別的相關資訊。 此資料表會針對每個類別 (例如 CPU 及其子類別) 顯示等候次數、等候時間和總等候時間的百分比。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活動|您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活動圖表存取不同層面的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活動。 您可以透過在 SQL 編譯/秒圖表線條上按一下某個點所取得的報表如下所示：<br /><br /> 連線和工作階段<br /><br /> Requests<br /><br /> 計畫快取命中率<br /><br /> tempdb 特性|  
  
## <a name="see-also"></a>另請參閱  
 [資料收集](data-collection.md)   
 [檢視收集組報表 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
  
