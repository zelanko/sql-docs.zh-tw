---
title: 健全狀況規則參考 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 47ae04ce-7b9d-49c2-8dbc-bafcb73d4603
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4eeb69baf54672514828591ffd4aa6c3dbc2610e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120768"
---
# <a name="health-rules-reference-powerpivot-for-sharepoint"></a>健全狀況規則參考 (PowerPivot for SharePoint)
  本參考主題描述 PowerPivot for SharePoint 安裝所加入的 SharePoint 健全狀況規則。 這些規則是用來報告伺服器健全狀況、可用性或 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服務應用程式組態或是其相關 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的問題。  
  
 下表根據這些規則出現在 SharePoint 管理中心的 [狀況分析規則定義] 頁面上的順序加以列出。 可設定的規則是您可以在觸發規則時變更臨界值的規則。 如需詳細資訊，請參閱 < [PowerPivot 健全狀況規則-設定](configure-power-pivot-health-rules.md)。 自動修復表示您可以從問題報告頁面按一下內建修復方法來解決問題。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 **注意：**[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 會針對不同版本的 SharePoint 安裝不同組的健全狀況規則。 請參閱下表的「版本」欄位，或者也可以執行以下 Windows PowerShell 命令來查看已安裝的規則。  
  
```  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like “*power*”}  | format-table -property * -autosize | out-default  
```  
  
|規則|可設定|自動修復|版本|描述|  
|----------|------------------|-----------------|-------------|-----------------|  
|PowerPivot：這部電腦上未安裝 Analysis Services OLE DB 提供者。|否|否|SharePoint 2010|Analysis Services OLE DB 提供者未安裝在伺服器上或是版本錯誤。 當您的 SharePoint 伺服器陣列包含在應用程式伺服器上沒有 PowerPivot for SharePoint 的 Excel Services 執行個體時，就會出現這個規則。 此規則會警告您 Excel Services 用來連接至 PowerPivot 資料的 Analysis Services OLE DB 提供者並未安裝。 若要解決此問題，請在沒有 Analysis Services OLE DB 提供者的每一部 Excel Services 伺服器上安裝 OLE DB 提供者。 您可以從 Microsoft 下載中心下載及安裝 Analysis Services OLE DB 提供者。 如需詳細資訊，請參閱 [Install the Analysis Services OLE DB Provider on SharePoint Servers](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。|  
|PowerPivot：當您在這部電腦上安裝 SQL Server 2008 R2 版本的 MSOLAP 提供者之後，Microsoft.AnalysisServices.ChannelTransport.dll 的登錄設定無效。|否|是|SharePoint 2010|這是伺服器組態問題。 最有可能是因為 ChannelTransport.dll 並未在全域組件中登錄。 請針對這個規則執行自動修復，在每部有安裝 PowerPivot for SharePoint 的伺服器上登錄此 .dll 檔。 此外，您也可以手動執行 regasm.exe 來登錄此檔案。 如果並未以本機管理員身分執行 SharePoint 計時器服務，則可能需要手動登錄。 無法更新登錄設定會造成 Excel Services 與 PowerPivot 系統服務之間的伺服器通訊緩慢，而且可能會造成某些安全性組態發生連接失敗。|  
|PowerPivot：PowerPivot 服務應用程式沒有完成作業的權限。|否|否|SharePoint 2010|這個規則會檢查 PowerPivot 服務應用程式識別是否為 PowerPivot 伺服器應用程式資料庫的資料庫擁有者，而且是否擁有本機 SQL Server Analysis Services 執行個體的管理權限。 系統會在安裝和部署期間自動授與這些權限，但如果這個步驟無法完成，將會發生此健全狀況規則。|  
|PowerPivot：PowerPivot 服務應用程式識別不應該是本機 Administrators 群組的成員。|否|否|SharePoint 2010|這是改善部署之整體安全性的最佳作法。 如果您已設定 PowerPivot 服務應用程式在屬於本機 Administrator 群組的帳戶之下執行，您應該將服務帳戶變更為不屬於該群組的帳戶。 建議您針對每一個服務使用最小權限的專用帳戶。 這樣做會讓服務隔離，並讓您更容易稽核登入。 如需變更服務帳戶的詳細資訊，請參閱[設定 PowerPivot 服務帳戶](configure-power-pivot-service-accounts.md)。|  
|PowerPivot：Analysis Services 執行個體以表格式模式執行，但指定這個模式的組態設定已關閉。|否|否|SharePoint 2010|這個規則會檢查 PowerPivot for SharePoint 安裝中的 SQL Server Analysis Services 執行個體是否將 `DeploymentMode` 伺服器屬性設定為 1。 如果此屬性設定為另一個值，或者執行規則檢查的 SharePoint 計時器服務沒有開啟檔案的權限，則這個規則將會失敗。 如需部署模式屬性的詳細資訊，請參閱 [判斷 Analysis Services 執行個體的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)。|  
|PowerPivot：PowerPivot 資料重新整理計時器工作已停用。|否|否|SharePoint 2013<br /><br /> SharePoint 2010|請檢查計時器工作設定以確認計時器工作已啟用。 如果您未使用 PowerPivot 資料重新整理功能，您可以忽略這個規則。 如需詳細資訊，請參閱 < [PowerPivot Data Refresh with SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)。|  
|PowerPivot：由 SQL Server 組態管理員所管理的 SQL Server Analysis Services (PowerPivot) 服務帳戶資訊與管理中心所管理的帳戶資訊不同。|否|否|SharePoint 2010|這個規則會檢查 SQL Server 組態管理員中的服務帳戶資訊是否與管理中心內相同 Analysis Services 執行個體所管理的帳戶資訊相同。 如果帳戶不同，則會在問題和解決方法報告中加入項目，好讓您可以將 SQL Server 組態管理員中的服務帳戶資訊變更回管理中心內指定的帳戶。 在變更 PowerPivot for SharePoint 安裝中的服務帳戶使用者名稱或密碼時，SQL Server 組態管理員並不是支援的工具。 使用管理中心會啟用 SharePoint 中所管理的帳戶。 更重要的是，如果您的伺服器陣列包含多部 PowerPivot for SharePoint 伺服器，則服務帳戶設定不一致可能會干擾擁有不正確服務資訊之伺服器上的處理和查詢作業。<br /><br /> 在單一伺服器上觸發這個規則時，PowerPivot 活頁簿會暫時運作，但是建議您最好盡快修復問題。 資料庫和檔案系統權限會使用管理中心內指定的帳戶資訊加以更新。|  
|PowerPivot：部署的伺服器陣列方案不是最新的。|否|是|SharePoint 2010|PowerPivot for SharePoint 安裝會使用伺服器陣列層級方案和 Web 應用程式層級方案來安裝其功能。 這個規則表示，伺服器陣列方案並不是最新的版本 (相較於伺服器或 Web 方案的版本)。 這最有可能是伺服器部署問題。 若要修復這個問題，請考慮執行 SQL Server 安裝程式來修復伺服器陣列中的其中一個 PowerPivot for SharePoint 安裝。 如需有關 PowerPivot for SharePoint 安裝中的解決方案的詳細資訊，請參閱[部署 PowerPivot 方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)。|  
|PowerPivot：CPU 整體使用量太高。|是|否|SharePoint 2010|此規則會報告系統層級的 CPU 耗用率。 CPU 整體使用量會受到監視，因為 PowerPivot 系統服務會使用 CPU 使用量做為伺服器健全狀況的量值，在伺服器陣列的多部 PowerPivot for SharePoint 伺服器中獲得健全狀況的負載平衡。 請考慮將另一部應用程式伺服器加入至伺服器陣列中，並將需要大量 CPU 的應用程式移到該伺服器。|  
|PowerPivot：Analysis Services 沒有足夠的 CPU 資源來執行要求的作業。|是|否|SharePoint 2010|提供給 Analysis Services 處理序 (msmdsrv.exe) 使用的 CPU 資源數量不夠此伺服器上的活動層級使用。 請考慮將另一部 PowerPivot for SharePoint 伺服器加入至伺服器陣列。 如需詳細資訊，請參閱 <<c0> [ 部署檢查清單： PowerPivot 伺服器加入 SharePoint 2010 伺服陣列的向外](../../sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)。|  
|PowerPivot：Analysis Services 沒有足夠的記憶體來執行要求的作業。|否|否|SharePoint 2010|當只剩下 5% 的可用記憶體可供 Analysis Services 使用時，就會觸發此規則。 在 SharePoint 應用程式伺服器上，SQL Server Analysis Services 執行個體應該一律擁有永遠是未使用的少量保留記憶體。 由於伺服器對於大部分的作業都會繫結記憶體，如果此伺服器一直都沒有執行到上限，則運作狀況會最好。<br /><br /> 根據預設，當可用記憶體縮減到 5% 以下時，就會發生記憶體不足的警告。 您可調整 Analysis Services 執行個體上的設定，將這個值變更為更高或更低的值。 如需詳細資訊，請參閱 < [PowerPivot 健全狀況規則-設定](configure-power-pivot-health-rules.md)。<br /><br /> 5% 的未使用記憶體會計算為配置給 Analysis Services 之記憶體的百分比。 例如，如果您的總記憶體為 200 GB，並將 80% 的記憶體 (或 160 GB) 配置給 Analysis Services，則 5% 的未使用記憶體為 160 GB 的 5% (或 8 GB)。|  
|PowerPivot：連接上限表示應該部署更多伺服器來處理目前的負載。|是|否|SharePoint 2010|根據預設，當相異使用者連接數目超過 100 時，就會觸發這個健全狀況規則。 這個預設值為任意值 (而不是根據伺服器的硬體規格或使用者活動)，所以您可能會根據您的環境中的伺服器容量和使用者活動來提高或降低此值。 如需詳細資訊，請參閱 < [PowerPivot 健全狀況規則-設定](configure-power-pivot-health-rules.md)。|  
|PowerPivot：將事件載入連接的比率太高。|是|否|SharePoint 2013<br /><br /> SharePoint 2010|根據預設，當載入事件對連接事件的百分比超過整個資料收集期間的 50% (預設為 4 小時) 時，就會觸發這個健全狀況規則。 這樣高的比率表示對唯一活頁簿的連接數目非常大，或者快取減少設定過於極端 (從系統中快速卸載和移除活頁簿，而該資料的要求仍在作用中)。 為了避免計算誤判數目，在可以計算比率之前，每 4 個小時的期間至少必須有 20 個連接。 您可以讓此健全狀況規則根據不同的比率。 如需詳細資訊，請參閱 < [PowerPivot 健全狀況規則-設定](configure-power-pivot-health-rules.md)。 如需有關設定快取的詳細資訊，請參閱 <<c0> [ 設定磁碟空間使用量&#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)。</c0>|  
|PowerPivot：在 Logs 目錄中找到一個或多個小型傾印檔案，表示程式損毀。|否|否|SharePoint 2013<br /><br /> SharePoint 2010|在程式損毀期間會產生小型傾印檔案，以擷取損毀之前有關 PowerPivot 服務應用程式狀態的資訊。 這項資訊可傳送給 Microsoft 並且用於疑難排解。 在伺服器上偵測到 .dmp 檔案時會觸發此規則。 此規則會提供該檔案的連結，您可以在 PowerPivot for SharePoint 執行個體的 \OLAP\Log 資料夾中找到此檔案。 請注意，您無法使用文字編輯器來檢視檔案內容。 檢視小型傾印檔案需要下載及安裝個別的偵錯工具。 如需詳細資訊，請參閱＜ [Windows 偵錯工具](http://go.microsoft.com/fwlink/?linkID=208266)＞。|  
|PowerPivot：快取 PowerPivot 資料所在之磁碟機上的磁碟空間不足。|是|否|SharePoint 2010|根據預設，當備份資料夾所在之磁碟機上的磁碟空間低於 5% 時，便會觸發此健全狀況規則。 如需有關設定此百分比的詳細資訊，請參閱 < [PowerPivot 健全狀況規則-設定](configure-power-pivot-health-rules.md)。 如需有關磁碟使用量的詳細資訊，請參閱 <<c0> [ 設定磁碟空間使用量&#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)。</c0>|  
|PowerPivot：無法以預期的頻率更新使用量資料。|是|否|SharePoint 2013<br /><br /> SharePoint 2010|PowerPivot for SharePoint 會使用內建的使用量資料收集系統來蒐集有關連接、資料重新整理以及查詢回應時間的度量。 它會將此使用量資料儲存在 PowerPivot 服務應用程式資料庫中，接著更新 PowerPivot 活頁簿 (PowerPivot Management Data.xlsx)，將資料提供給 PowerPivot 管理儀表板中的報表。 這個規則表示使用量資料並未以足夠的頻率移到 PowerPivot Management Data.xlsx 檔案中。 此規則會使用 .xlsx 檔案上的時間戳記當做檔案已更新的證明。 如果破壞資料精確度的使用量資料收集系統中有其他問題，這個規則將不會偵測到。 若要針對這個錯誤進行疑難排解，請檢查計時器工作以確認這些工作正在執行。 如需有關使用量資料收集的詳細資訊，請參閱 <<c0> [ 設定使用量資料收集的&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。</c0>|  
|PowerPivot：MidTier 處理帳戶應該對所有關聯的 SPWebApplications 具有「完整讀取」權限。|否|是|SharePoint 2013<br /><br /> SharePoint 2010|PowerPivot 服務應用程式識別必須擁有**完整讀取**權限，才能存取 SharePoint 內容資料庫，代表擁有文件中的 僅檢視 」 權限的使用者。 若要判斷哪一個帳戶當做 PowerPivot 服務應用程式識別，請開啟**來設定服務帳戶**在 [管理中心] 頁面。 服務應用程式最有可能在 **[SharePoint Web 服務系統]** 服務應用程式集區或專用應用程式集區內執行。 雖然這項規則提供了自動修復選項，您會獲得更好的結果，如果您手動授與權限執行下列動作：<br /><br /> 1) 在管理中心按一下 [管理 Web 應用程式]。<br /><br /> 2) 選取網站，然後按一下 [使用者原則]。<br /><br /> 3) 按一下 [加入使用者]。<br /><br /> 4) 選取 [(所有區域)]，然後按一下 [下一步]。<br /><br /> 5） 在 [使用者] 中，輸入 PowerPivot 服務應用程式識別，然後按一下**完整讀取**核取方塊。 按一下 **[完成]**。<br /><br /> 6) 驗證修復。 在 [監視] 中，按一下 **[檢閱規則定義]**。 尋找然後開啟 PowerPivot 規則。 按一下 **[立即執行]**。 返回 **[檢閱問題與方案]** ，確認規則不再出現。|  
|PowerPivot：Secondary Logon 服務 (seclogon) 已停用|否|否|SharePoint 2013<br /><br /> SharePoint 2010|Secondary Logon 服務可用來在 PowerPivot 圖庫中產生 PowerPivot 活頁簿的縮圖影像。 Secondary Logon 服務預設會設定為手動啟動。 如果停用服務，產生縮圖的作業會失敗。 此外，ULS 記錄檔會包含下列錯誤：「錯誤 1058 可做為 Windows 服務 “Secondary Logon” 已停用的根本原因。」(The error 1058 can have as a root cause the fact the Windows service “Secondary Logon” is disabled.)<br /><br /> 若要檢查服務組態，請使用 [服務] 主控台應用程式尋找 Secondary Logon，然後將其 **[啟動類型]** 變更為 **[手動]**。 如果無法啟用服務，您的組織可能具有停用服務的群組原則。 請與管理員聯繫，確定是否為此情況。<br /><br /> 啟用服務之後，縮圖或快照影像會每隔一段時間重新整理。 或者，您可以重新啟動服務，然後開啟再重新儲存特定報表的屬性頁面，藉此強制重新整理。 如需詳細資訊，請參閱 <<c0> [ 如何使用 PowerPivot 圖庫](http://go.microsoft.com/fwlink/?LinkId=246462)。|  
|PowerPivot：ADOMD.NET 不是安裝在為管理中心設定的獨立 WFE 上|否|否|SharePoint 2013<br /><br /> SharePoint 2010|ADOMD.NET 是支援連接至 Analysis Services 資料庫的 Analysis Services 用戶端程式庫。 在 PowerPivot for SharePoint 部署中，ADOMD.NET 可從管理中心的 PowerPivot 管理儀表板存取內建報表。 內建報表實際上是包含內嵌 Analysis Services 資料的 PowerPivot 活頁簿。 管理儀表板使用 ADOMD.NET 將連接要求傳送至伺服器，以載入活頁簿中包含的資料。<br /><br /> 在其管理中心於獨立 Web 前端伺服器上執行的拓撲中，若要在管理儀表板中檢視這些報表，您必須手動安裝 ADOMD.NET。 如需詳細資訊，請參閱 [在執行管理中心的 Web 前端伺服器上安裝 ADOMD.NET](../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)。|  
  
  
