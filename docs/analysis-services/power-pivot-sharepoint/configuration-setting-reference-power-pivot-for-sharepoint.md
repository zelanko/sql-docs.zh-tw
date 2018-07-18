---
title: 組態設定參考 (Power Pivot for SharePoint) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e2da78373d8bcb613bb11dca54857bc7b98dfe1
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982610"
---
# <a name="configuration-setting-reference-power-pivot-for-sharepoint"></a>組態設定參考 (PowerPivot for SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本主題提供 SharePoint 伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式所使用的組態設定參考文件。 如果您使用 PowerShell 指令碼來設定伺服器，或者，如果想查閱特定設定的資訊，本主題中的資訊提供詳細的說明。  
  
 組態設定是為每個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式設定。 在伺服陣列中，您可以建立多個服務應用程式，做為設定相同實體服務執行個體之獨立邏輯執行個體的一種方式。 組態設定會儲存在為您所設定每個服務應用程式建立的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 應用程式資料庫中。  
  
 如果您變更組態設定，變更會立即生效並用於後續的要求和連接。 進行中的作業是由在作業開始時起作用的設定來規範。  
  
 按下列連結，可閱讀特定設定區域的相關資訊：  
  
 [資料載入逾時](#LoadingData)  
  
 [連接集區](#ConnectionPool)  
  
 [負載平衡](#AllocationScheme)  
  
 [資料重新整理](#DataRefresh)  
  
 [使用量資料收集](#UsageData)  
  
 如需如何建立 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式的指示，請參閱 [在管理中心建立和設定 Power Pivot 服務應用程式](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)。  
  
##  <a name="LoadingData"></a> 資料載入逾時  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料是由在伺服器陣列中的 Analysis Services 伺服器執行個體擷取及載入。 依上次存取資料的時間與方式而定，會從內容庫或本機檔案快取載入。 只要接到查詢或處理要求，資料就會載入記憶體中。 為了提供最大的整體伺服器可用性，如果無法在配置的時間內完成，您可以設定逾時值，指示伺服器停止載入資料要求。  
  
|名稱|預設|有效的值|描述|  
|----------|-------------|------------------|-----------------|  
|資料載入逾時|1800 (秒)|1 到 3600|指定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式等候特定 Analysis Services 伺服器執行個體回應的時間。<br /><br /> 在預設情況下，服務應用程式會在將特定要求轉送給 Engine 後等待 30 分鐘，讓 Engine 服務執行個體傳來資料裝載。<br /><br /> 如果 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源無法在這段時間內載入，執行緒將會停止，並啟動新的執行緒。|  
  
##  <a name="ConnectionPool"></a> 連接集區  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式會建立並管理連接集區，以便重複使用連接。 連接集區有兩種類型：一種是唯讀資料的資料連接，另一種是伺服器連接。  
  
 資料連接集區包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源的快取連接。 每個連接集區都是以載入資料庫時設定的內容為根據。 此內容包含實體服務執行個體的識別、資料庫識別碼，以及要求資料之 SharePoint 使用者的識別。 每個組合都會建立不同的連接集區。 例如，不同使用者對相同伺服器上所執行相同資料庫的要求會取用不同集區的連接。  
  
 連接集區的目的是讓相同 SharePoint 使用者對相同 Analysis Services 資料庫所提出的唯讀要求使用快取連接。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行個體是記憶體中已載入資料的伺服器。 資料庫識別碼是資料模型 (具現化為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 資料庫的模型) 之記憶體中資料結構的內部識別碼。 版本資訊會以隱含方式納入識別碼中。  
  
 伺服器連接集區包含從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式執行個體至 Analysis Services 伺服器執行個體的快取連接，這是由服務應用程式以 Analysis Services 伺服器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系統管理員權限進行連接。 這些連接是用來發出載入資料庫要求，並監視系統健全狀況。  
  
 每一種連接集區都有您可以設定的上限，確保以最佳方式使用系統記憶體來管理連接。  
  
|名稱|預設|有效的值|描述|  
|----------|-------------|------------------|-----------------|  
|連接集區逾時|1800 (秒)|1 到 3600。|此設定會套用至資料連接集區。<br /><br /> 它會指定閒置的連接在移除之前，可以保留在連接集區中的時間。<br /><br /> 在預設情況下，如果連接閒置超過五分鐘，服務應用程式就會移除連接。|  
|最大使用者連接集區大小|1000|-1、0 或 1 到 10000。<br /><br /> -1 指定無限數目的閒置連接。<br /><br /> 0 表示不保留閒置的連接。 每次都必須建立新的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源連接。|此設定會套用至為特定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式執行個體建立之所有資料連接集區中的閒置連接數。<br /><br /> 個別連接集區是針對 SharePoint 使用者、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料和服務執行個體之獨特組合所建立。 如果您有許多使用者存取各種不同的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源，伺服器的效能可能會因連接集區大小增加而受益。<br /><br /> 如果有超過 100 個閒置的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行個體連接，則新閒置的連接會中斷連接，而不會再傳回集區。|  
|最大管理連接集區大小|200|-1、0 或 1 到 10000。<br /><br /> -1 指定無限數目的閒置連接。|在所有管理連接集區中，為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式與 Analysis Services 伺服器執行個體之連接所建立的閒置伺服器連接數上限。 伺服器連接是用於載入資料庫的要求，並將變更存回 SharePoint 資料庫。|  
  
##  <a name="AllocationScheme"></a> 負載平衡  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行的其中一項功能是，判斷在可用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務執行個體中，Analysis Services 資料將載入的位置。 **AllocationMethod** 設定會指定選取服務執行個體的準則。  
  
|名稱|預設|有效的值|描述|  
|----------|-------------|------------------|-----------------|  
|配置方法|循環配置資源|循環配置資源<br /><br /> 依據健全狀態|在兩個或多個 Analysis Services 伺服器執行個體中，配置載入要求的方案。<br /><br /> 根據預設， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務將會根據伺服器健全狀況替代要求。 依據健全狀況則根據可用的記憶體和 CPU 使用率，配置要求給具有最多可用系統資源的伺服器。<br /><br /> 循環配置資源會依照順序在可用伺服器之間輪流配置要求，而不考慮目前的負載或伺服器健全狀況。|  
  
##  <a name="DataRefresh"></a> 資料重新整理  
 指定時間範圍定義您組織中正常或一般工作日。 這些組態設定會決定下班後資料處理進行資料重新整理作業的時間。 下班後處理可以從工作日結束時間開始。 文件擁有者若想要利用在正常上班時間內所產生的交易資料重新整理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源，下班後處理就是這些文件擁有者的排程選項。  
  
|名稱|預設|有效的值|描述|  
|----------|-------------|------------------|-----------------|  
|開始時間|上午 04:00|1 至 12 小時，其中的值是該範圍內的有效整數。<br /><br /> 類型是 Time。|設定上班時間範圍的下限。|  
|結束時間|下午 08:00|1 至 12 小時，其中的值是該範圍內的有效整數。<br /><br /> 類型是 Time。|設定上班時間範圍的上限。|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 無人看管的資料重新整理帳戶|無|目標應用程式識別碼|此帳戶用來代表排程擁有者執行資料重新整理作業。<br /><br /> 自動資料重新整理必須事先加以定義，才能在服務應用程式組態頁面參考。 如需詳細資訊，請參閱 [設定 Power Pivot 無人看管的資料重新整理帳戶 (Power Pivot for SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493)。|  
|允許使用者輸入自訂的 Windows 認證|已啟用|布林|決定排程的資料重新整理組態頁面是否顯示允許排程擁有者指定 Windows 使用者帳戶與密碼來執行資料重新整理作業的選項。<br /><br /> 您必須啟用 Secure Store Service，此選項才能運作。 如需詳細資訊，請參閱 [設定 Power Pivot 資料重新整理的預存認證 (Power Pivot for SharePoint)](http://msdn.microsoft.com/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)。|  
|最大處理記錄長度|365|1 到 5000 天|決定資料重新整理歷程記錄要保留在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式資料庫中的時間長度。 如需詳細資訊，請參閱 [Power Pivot 使用量資料收集](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)。|  
  
##  <a name="UsageData"></a> 使用量資料收集  
 出現在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板中的使用方式報表可以提供有關如何使用啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]功能之活頁簿的重要資訊。 下列組態設定會控制 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器事件的使用量資料收集層面 (後續將呈現於使用方式或活動報表中)。  
  
|名稱|預設|有效的值|描述|  
|----------|-------------|------------------|-----------------|  
|查詢報告間隔|300 (以秒為單位)|1 到 n 秒，其中 n 是任何有效的整數。|為了確保使用量資料收集不會耗用太多伺服陣列的資料傳輸容量，查詢統計資料是在每個連接上收集，並報告為單一事件。 「查詢報告間隔」會決定報告事件的頻率。 在預設情況下，查詢統計資料會每隔 5 分鐘報告一次。<br /><br /> 由於連接是一傳送要求就立即關閉，所以即使是單一使用者存取單一 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源，系統也會為該使用者產生大量的連接。 因此，連接集區會針對每個使用者和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源而建立，以便在建立連接後，讓相同的使用者能夠對相同的資料重複使用該連接。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式會依透過此組態設定指定的間隔，定期報告連接集區中每個連接的使用量資料。<br /><br /> 提高報告時間間隔值會使得記錄的事件較少。 但是，如果設得太高，當伺服器重新啟動或連接關閉時，就會有遺失事件資料的風險。<br /><br /> 降低此值會導致以較高頻率記錄更多事件，而將更多 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]相關使用量資料加入 SharePoint 使用量資料庫的資料收集系統。<br /><br /> 一般來說，除非您嘗試要解決特定問題 (例如，由於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 使用量資料的結果，讓使用量資料庫成長太快)，否則請勿變更此組態設定。|  
|使用量資料記錄|365 (以天為單位)|0 或 1 到 n 天，其中 n 是任何有效的整數。<br /><br /> 0 表示永遠保留記錄，而且永遠不刪除。|根據預設，使用量資料會在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式資料庫中保留一年。 超過一年的記錄會從資料庫卸除。<br /><br /> Microsoft SharePoint Foundation 使用量資料處理作業執行時，會每天檢查過期的記錄資料。 計時器作業會讀取此設定，並觸發 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式資料庫中過期記錄的資料刪除命令。|  
|簡單式回應時間上限|500 (以毫秒為單位)|1 到 n 毫秒，其中 n 是任何有效的整數。|在預設情況下，簡單式查詢的臨界值是半秒。<br /><br /> 簡單式查詢包括伺服器 Ping、要求中繼資料，以及啟動工作階段。|  
|快速回應時間上限|1000 (以毫秒為單位)|1 到 n 毫秒，其中 n 是任何有效的整數。|在預設情況下，快速要求的臨界值是一秒。<br /><br /> 快速要求是具有極小資料集的要求，或跨越大量成員集的中繼資料要求。|  
|預期回應時間上限|3000 (以毫秒為單位)|1 到 n 毫秒，其中 n 是任何有效的整數。|在預設情況下，預期要求的臨界值是三秒。<br /><br /> 此臨界值設定預期查詢時間的上限。|  
|長回應時間上限|10000 (以毫秒為單位)|1 到 n 毫秒，其中 n 是任何有效的整數。|在預設情況下，長時間要求的臨界值是十秒。<br /><br /> 這些要求的執行時間比預期還長，但仍在可接受的範圍內。|  
  
## <a name="see-also"></a>另請參閱  
 [在管理中心建立和設定 Power Pivot 服務應用程式](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Power Pivot 資料重新整理與 SharePoint 2010](http://msdn.microsoft.com/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [設定使用量資料收集的對象 &#40;Power Pivot for SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [設定 Power Pivot 服務帳戶](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Power Pivot 管理儀表板和使用量資料](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)  
  
  
