---
title: PowerPivot 驗證及授權 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f28da387576eee3d9619e4fc817485beb5c8662
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377858"
---
# <a name="powerpivot-authentication-and-authorization"></a>PowerPivot 驗證及授權
  在 SharePoint 2010 伺服陣列中執行的 PowerPivot for SharePoint 部署會使用 SharePoint 伺服器所提供的驗證子系統和授權模型。 由於所有 PowerPivot 相關的內容都儲存在 SharePoint 內容資料庫中，而且 PowerPivot 相關的所有作業都在伺服器陣列中的 PowerPivot 共用服務上執行，SharePoint 安全性基礎結構會延伸到 PowerPivot 內容和作業。 使用者若要求包含 PowerPivot 資料的活頁簿，就會使用以其 Windows 使用者識別為基礎的 SharePoint 使用者識別進行驗證。 活頁簿上的檢視權限會決定授與或拒絕要求。  
  
 由於自助式資料分析必須與 Excel Services 整合，所以您也必須了解 Excel Services 安全性，才能保護 PowerPivot 伺服器的安全。 當使用者查詢具有 PowerPivot 資料之資料連接的樞紐分析表時，Excel Services 會轉送資料連接要求到伺服陣列中的 PowerPivot 伺服器以載入資料。 您必須了解如何設定這兩部伺服器的安全性設定，才能進行伺服器間的互動。  
  
 按下列連結可閱讀本主題中的特定小節：  
  
 [使用傳統模式登入的 Windows 驗證需求](power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [PowerPivot 作業需要使用者授權](#UserConnections)  
  
 [PowerPivot 資料存取的 SharePoint 權限](#Permissions)  
  
 [PowerPivot 活頁簿的的 Excel Services 安全性考量](#excel)  
  
##  <a name="bkmk_auth"></a> 使用傳統模式登入的 Windows 驗證需求  
 PowerPivot for SharePoint 支援 SharePoint 所提供之一組經過簡化的驗證選項。 在所有可用的驗證選項中，PowerPivot for SharePoint 部署僅支援 Windows 驗證。 此外，發生登入的 Web 應用程式必須設定為使用傳統模式。  
  
 由於 PowerPivot for SharePoint 部署的 Analysis Services 資料引擎僅支援 Windows 驗證，因此需要 Windows 驗證。 Excel Services 使用透過 NTLM 或 Kerberos 通訊協定驗證的 Windows 使用者識別，經由 MSOLAP OLE DB 提供者建立 Analysis Services 連接。  
  
 第二個需求是 Web 應用程式上必須使用傳統模試驗證，以確保 PowerPivot Web 服務可操作。 Web 服務是在 Web 前端上執行的元件，並提供伺服器陣列中的 SharePoint 伺服器 PowerPivot 的 HTTP 重新導向。 Web 服務是服務對服務通訊的宣告感知 (Claims-Aware) 服務，但不是路由傳送至伺服器陣列中 PowerPivot 共用服務之資料連接要求的宣告感知 (Claims-Aware) 服務。 只有來自使用 Windows 識別之 IIS 的驗證連接，才支援載入 PowerPivot 資料的要求。 在 Web 應用程式上使用傳統模試登入，可確保從 PowerPivot Web 服務成功連接至伺服器陣列中的 PowerPivot 共用服務。  
  
 雖然較常見的資料存取案例 (從轉譯 PowerPivot 資料的相同 Excel 活頁簿中擷取資料) 不需要使用傳統模式登入，不過請勿嘗試使用 PowerPivot for SharePoint 搭配設定為使用其他驗證提供者的 SharePoint Web 應用程式。 這樣做會在使用者每次嘗試連接至 PowerPivot 活頁簿做為外部資料來源時，導致連接失敗。  
  
 如果未使用傳統模式登入，則 PowerPivot Web 服務所處理的下列類型要求會失敗：  
  
-   對來自伺服器陣列外的 PowerPivot 資料的任何要求 (例如，在報表設計師或報表產生器中建立報表，其中資料來源為指向 PowerPivot 活頁簿的 SharePoint URL)  
  
-   來自用戶端應用程式或報表的伺服器陣列內要求，該應用程式或報表使用 PowerPivot 活頁簿做為外部資料來源 (例如，在 Excel 桌面應用程式中建立活頁簿，並將另一個包含 PowerPivot 資料的已發佈 Excel 活頁簿做為您的資料來源)  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>如何檢查應用程式的驗證提供者  
 建立新的 Web 應用程式時，請務必在 [建立新 Web 應用程式] 頁面中選取 **[傳統模式驗證]** 選項。  
  
 若為現有的 Web 應用程式，請使用下列指示來確認 Web 應用程式是否設定為使用 Windows 驗證。  
  
1.  在管理中心的 [應用程式管理] 中，按一下 **[管理 Web 應用程式]**。  
  
2.  選取 Web 應用程式。  
  
3.  按一下 **[驗證提供者]**。  
  
4.  確認每個區域都有一個提供者，而且預設區域設為 Windows。  
  
##  <a name="UserConnections"></a> PowerPivot 作業需要使用者授權  
 SharePoint 授權只用於 PowerPivot 查詢和資料處理的所有層級存取。  
  
 不支援 Analysis Services 以角色為基礎的授權模型。 資料格、資料列或資料表層級的 PowerPivot 資料無法使用以角色為基礎的授權。 您無法透過保護活頁簿不同部分的安全，在其中為特定的使用者授與或拒絕機密資料的存取。 擁有 SharePoint 文件庫中 Excel 活頁簿之檢視權限的使用者可以完整使用內嵌的 PowerPivot 資料。  
  
 PowerPivot for SharePoint 會模擬下列案例中的 SharePoint 使用者：  
  
-   查詢具有 PowerPivot 資料庫之資料連接的樞紐分析表或樞紐分析圖，在其中 PowerPivot 服務應用程式會代表使用者建立連接到處理資料的特定 PowerPivot 共用服務執行個體。  
  
-   如果沒有可用的資料，從快取或文件庫載入 PowerPivot 資料。 如果對尚未載入系統中的 PowerPivot 資料要求資料連接，[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]執行個體會使用 SharePoint 使用者識別，從內容庫擷取資料來源，並載入記憶體中。  
  
-   將資料來源的更新複本儲存至內容庫中活頁簿的資料重新整理作業。 在此情況下，實際登入作業是使用從 Secure Store Service 之目標應用程式擷取的使用者名稱和密碼執行。 認證可以是 PowerPivot 無人看管的資料重新整理帳戶，或以資料建立時，其重新整理排程儲存的認證。 如需詳細資訊，請參閱 < [PowerPivot 資料重新整理設定的預存認證&#40;PowerPivot for SharePoint&#41; ](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)並[設定 PowerPivot 無人看管資料重新整理帳戶&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。  
  
##  <a name="Permissions"></a> PowerPivot 資料存取的 SharePoint 權限  
 發行、管理及保護 PowerPivot 活頁簿安全等作業只透過 SharePoint 整合進行支援。 SharePoint 伺服器提供確保合法存取資料的驗證和授權子系統。 在 SharePoint 伺服器陣列之外安全部署 PowerPivot 活頁簿，並沒有支援案例。  
  
 使用者可透過「檢視」權限或更高的權限來存取 PowerPivot 資料，且此使用者存取在伺服器上是唯讀的。 「參與」權限允許加入及編輯檔案。 您必須將活頁簿下載至安裝 PowerPivot for Excel 的 Excel 桌面應用程式，才可以變更 PowerPivot 資料。 檔案的「參與」權限決定使用者是否可以在本機下載檔案，然後再將變更儲存回 SharePoint 中。  
  
 在此情況下，「參與」和「僅檢視」層級權限會定義有效的 PowerPivot 資料使用者存取權限集。 其他權限層級的有效層級最高與「參與」和「僅檢視」權限相同 (例如，由於「讀取」包含「僅檢視」權限，指派「讀取」權限的使用者也會擁有與「僅檢視」相同的存取層級)。  
  
 下表摘要說明決定對 PowerPivot 資料和伺服器作業存取的權限層級：  
  
|權限等級|允許下列工作|  
|----------------------|------------------------|  
|伺服陣列或服務管理員|安裝、啟用與設定服務和應用程式。<br /><br /> 使用 PowerPivot 管理儀表板與檢視管理報表。|  
|完整控制|啟用網站集合層級的 PowerPivot 功能整合。<br /><br /> 建立 PowerPivot 圖庫文件庫。<br /><br /> 建立資料摘要庫。|  
|參與|加入、編輯、刪除與下載 PowerPivot 活頁簿。<br /><br /> 設定資料重新整理。<br /><br /> 根據 SharePoint 網站上的 PowerPivot 活頁簿，建立新的活頁簿和報表。<br /><br /> 在資料摘要庫中建立資料服務文件|  
|讀取|做為外部資料來源，其中活頁簿 URL 明確輸入 （例如，在 Excel 的資料連接精靈） 的 [連線] 對話方塊中存取 PowerPivot 活頁簿。|  
|僅檢視|檢視 PowerPivot 活頁簿。<br /><br /> 檢視資料重新整理記錄。<br /><br /> 將本機活頁簿連接至 SharePoint 網站上的 PowerPivot 活頁簿，以其他方式重新訂定其資料用途。<br /><br /> 下載活頁簿的快照集。 此快照集是資料的靜態複本，不包含交叉分析篩選器、篩選、公式或資料連接。 此快照集的內容類似於從瀏覽器視窗中複製資料格值。|  
  
##  <a name="excel"></a> PowerPivot 活頁簿的的 Excel Services 安全性考量  
 PowerPivot 伺服器端查詢處理與 Excel Services 緊密結合。 產品整合開始於文件層級，在此層級中，PowerPivot 活頁簿是包含或參考 PowerPivot 資料的 Excel 活頁簿 (.xlsx) 檔案。 PowerPivot 活頁簿沒有個別的副檔名。  
  
 在 SharePoint 網站上開啟 PowerPivot 活頁簿時，Excel Services 會讀取內嵌的 PowerPivot 資料連接字串，並將要求轉送至本機 SQL Server Analysis Services OLE DB 提供者。 接著，此提供者會將連接資訊傳遞到伺服器陣列中的 PowerPivot 伺服器。 若要讓要求在兩部伺服器間順暢地流動，必須將 Excel Services 設定為使用 PowerPivot for SharePoint 所需的設定。  
  
 在 Excel Services 中，您可以針對信任的位置、信任的資料提供者以及信任的資料連線庫指定安全性相關的組態設定。 下表將描述啟用或強化 PowerPivot 資料存取的設定。 如果有設定未列在此處，對 PowerPivot 伺服器連接並沒有影響。 如需有關如何指定這些設定的逐步指示，請參閱 < 啟用 Excel Services > 一節中[初始設定&#40;PowerPivot for SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)。  
  
> [!NOTE]  
>  與安全性最相關的設定會套用至信任的位置。 如果您要保留預設值或在不同的網站使用不同的值，您可以針對包含 PowerPivot 資料的網站建立其他信任的位置，然後只針對該網站進行下列設定。 如需相關資訊，請參閱 [在管理中心建立 PowerPivot 網站的信任位置](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
|區域|設定|描述|  
|----------|-------------|-----------------|  
|Web 應用程式|Windows 驗證提供者|PowerPivot 會將它從 Excel Services 取得的宣告 Token 轉換為 Windows 使用者識別。 將 Excel Services 當做資源使用的所有 Web 應用程式都必須設定為使用 Windows 驗證提供者。|  
|信任的位置|位置類型|此值必須設為 **[Microsoft SharePoint Foundation]**。 PowerPivot 伺服器會擷取 .xlsx 檔案的複本，並將其載入伺服陣列中的 Analysis Services 伺服器。 伺服器只能從內容庫擷取 .xlsx 檔。|  
||允許外部資料|此值必須設為 **[信任的資料連線庫與內嵌連線]**。 PowerPivot 資料連接內嵌在活頁簿中。 如果您不允許內嵌連接，使用者可以檢視 PivotTable 快取，但是他們將無法與 PowerPivot 資料進行互動。|  
||重新整理時警告|如果您要使用 PowerPivot 圖庫儲存活頁簿與報表，應該停用此值。 PowerPivot 圖庫包含文件預覽功能，開啟時重新整理與重新整理時警告同時關閉時效果最好。|  
|信任的資料提供者|MSOLAP.4<br /><br /> MSOLAP.5|預設隨附 MSOLAP.4，但是 PowerPivot 資料存取需要 MSOLAP.4 提供者為 SQL Server 2008 R2 版。<br /><br /> MSOLAP.5 會隨 PowerPivot for SharePoint 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版安裝。<br /><br /> 請不要從信任的資料提供者清單中移除這些提供者。 在某些情況下，您可能需要在伺服器陣列中的其他 SharePoint 伺服器上，安裝此提供者的額外複本。 如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。|  
|信任的資料連線庫|選擇性。|您可以使用 PowerPivot 活頁簿中的 Office 資料連線 (.odc) 檔案。 如果您使用 .odc 檔案來提供本機 PowerPivot 活頁簿的連接資訊，就可以將相同的 .odc 檔案加入至這個連線庫。|  
|使用者定義函數組件|不適用。|PowerPivot for SharePoint 會忽略您為 Excel Services 建立部署的使用者定義函數組件。 如果您依賴使用者定義的組件執行特定行為，請注意 PowerPivot 查詢處理不會使用您建立的使用者定義函數。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 PowerPivot 服務帳戶](configure-power-pivot-service-accounts.md)   
 [設定 PowerPivot 無人看管的資料重新整理帳戶&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [在管理中心建立 PowerPivot 網站的信任的位置](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [PowerPivot 安全性架構](https://go.microsoft.com/fwlink/?linkID=220970)  
  
  
