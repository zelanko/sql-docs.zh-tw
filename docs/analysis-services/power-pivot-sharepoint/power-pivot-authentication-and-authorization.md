---
title: Power Pivot 驗證和授權 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 710db3b55eb8e3bd1e885dfd71e2bde15360092c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-authentication-and-authorization"></a>PowerPivot 驗證及授權
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 SharePoint 2010 伺服陣列中執行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署會使用 SharePoint 伺服器所提供的驗證子系統和授權模型。 由於所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 相關的內容都儲存在 SharePoint 內容資料庫中，而且 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]相關的所有作業都在伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]共用服務上執行，因此 SharePoint 安全性基礎結構會延伸到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 內容和作業。 使用者若要求包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的活頁簿，就會使用以其 Windows 使用者識別為基礎的 SharePoint 使用者識別進行驗證。 活頁簿上的檢視權限會決定授與或拒絕要求。  
  
 由於自助式資料分析必須與 Excel Services 整合，所以您也必須了解 Excel Services 安全性，才能保護 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器的安全。 當使用者查詢具有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料之資料連接的樞紐分析表時，Excel Services 會轉送資料連接要求到伺服陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器以載入資料。 您必須了解如何設定這兩部伺服器的安全性設定，才能進行伺服器間的互動。  
  
 按下列連結可閱讀本主題中的特定小節：  
  
 [使用傳統模式登入的 Windows 驗證需求](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Power Pivot 作業需要使用者授權](#UserConnections)  
  
 [Power Pivot 資料存取的 SharePoint 存取權限](#Permissions)  
  
 [PowerPivot 活頁簿的 Excel Services 安全性考量](#excel)  
  
##  <a name="bkmk_auth"></a> 使用傳統模式登入的 Windows 驗證需求  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 支援 SharePoint 所提供之一組經過簡化的驗證選項。 在所有可用的驗證選項中， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署僅支援 Windows 驗證。 此外，發生登入的 Web 應用程式必須設定為使用傳統模式。  
  
 由於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署的 Analysis Services 資料引擎僅支援 Windows 驗證，因此需要 Windows 驗證。 Excel Services 使用透過 NTLM 或 Kerberos 通訊協定驗證的 Windows 使用者識別，經由 MSOLAP OLE DB 提供者建立 Analysis Services 連接。  
  
 第二個需求是 Web 應用程式上必須使用傳統模試驗證，以確保 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Web 服務可操作。 Web 服務是在 Web 前端上執行的元件，並在伺服器陣列中提供對 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器的 HTTP 重新導向。 Web 服務是服務對服務通訊的宣告感知 (Claims-Aware) 服務，但不是路由傳送至伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共用服務之資料連接要求的宣告感知 (Claims-Aware) 服務。 只有來自使用 Windows 識別之 IIS 的驗證連接，才支援載入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的要求。 在 Web 應用程式上使用傳統模試登入，可確保從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Web 服務成功連接至伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共用服務。  
  
 雖然較常見的資料存取案例 (從轉譯 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的相同 Excel 活頁簿中擷取資料) 不需要使用傳統模式登入，不過請勿嘗試使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 搭配已設定為使用其他驗證提供者的 SharePoint Web 應用程式。 這樣做會在使用者每次嘗試連接至 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿做為外部資料來源時，導致連接失敗。  
  
 如果未使用傳統模式登入，則 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Web 服務所處理的下列類型要求會失敗：  
  
-   對來自伺服器陣列外的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的任何要求 (例如，在報表設計師或報表產生器中建立報表，其中資料來源為指向 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的 SharePoint URL)  
  
-   來自用戶端應用程式或報表的伺服器陣列內要求，該應用程式或報表使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿作為外部資料來源 (例如，在 Excel 桌面應用程式中建立活頁簿，並將另一個包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的已發佈 Excel 活頁簿做為您的資料來源)  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>如何檢查應用程式的驗證提供者  
 建立新的 Web 應用程式時，請務必在 [建立新 Web 應用程式] 頁面中選取 **[傳統模式驗證]** 選項。  
  
 若為現有的 Web 應用程式，請使用下列指示來確認 Web 應用程式是否設定為使用 Windows 驗證。  
  
1.  在管理中心的 [應用程式管理] 中，按一下 **[管理 Web 應用程式]**。  
  
2.  選取 Web 應用程式。  
  
3.  按一下 **[驗證提供者]**。  
  
4.  確認每個區域都有一個提供者，而且預設區域設為 Windows。  
  
##  <a name="UserConnections"></a> Power Pivot 作業需要使用者授權  
 SharePoint 授權只用於對 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查詢和資料處理的所有層級存取。  
  
 不支援 Analysis Services 以角色為基礎的授權模型。 資料格、資料列或資料表層級的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料無法使用以角色為基礎的授權。 您無法透過保護活頁簿不同部分的安全，在其中為特定的使用者授與或拒絕機密資料的存取。 擁有 SharePoint 文件庫中 Excel 活頁簿之檢視權限的使用者可以完整使用內嵌的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 會模擬下列案例中的 SharePoint 使用者：  
  
-   查詢具有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫之資料連接的樞紐分析表或樞紐分析圖，在其中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式會代表使用者建立連接到處理資料的特定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共用服務執行個體。  
  
-   如果沒有可用的資料，從快取或文件庫載入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料。 如果對尚未載入系統中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料要求資料連接， [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 執行個體會使用 SharePoint 使用者識別，從內容庫擷取資料來源，並載入記憶體中。  
  
-   將資料來源的更新複本儲存至內容庫中活頁簿的資料重新整理作業。 在此情況下，實際登入作業是使用從 Secure Store Service 之目標應用程式擷取的使用者名稱和密碼執行。 認證可以是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 無人看管的資料重新整理帳戶，或以資料建立時，其重新整理排程儲存的認證。 如需詳細資訊，請參閱 [設定 Power Pivot 資料重新整理的預存認證 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75) 和 [設定 Power Pivot 無人看管的資料重新整理帳戶 (PowerPivot for SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)。  
  
##  <a name="Permissions"></a> Power Pivot 資料存取的 SharePoint 存取權限  
 發行、管理及保護 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿安全等作業只透過 SharePoint 整合進行支援。 SharePoint 伺服器提供確保合法存取資料的驗證和授權子系統。 並沒有支援案例可用於在 SharePoint 伺服器陣列之外安全部署 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿。  
  
 使用者可透過「檢視」權限或更高的權限來存取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料，且此使用者存取在伺服器上是唯讀的。 「參與」權限允許加入及編輯檔案。 您必須將活頁簿下載至安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 的 Excel 桌面應用程式，才可以變更 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料。 檔案的「參與」權限決定使用者是否可以在本機下載檔案，然後再將變更儲存回 SharePoint 中。  
  
 在此情況下，「參與」和「僅檢視」層級權限會定義有效的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料使用者存取權限集。 其他權限層級的有效層級最高與「參與」和「僅檢視」權限相同 (例如，由於「讀取」包含「僅檢視」權限，指派「讀取」權限的使用者也會擁有與「僅檢視」相同的存取層級)。  
  
 下表摘要說明決定對 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料和伺服器作業存取的權限層級：  
  
|權限等級|允許下列工作|  
|----------------------|------------------------|  
|伺服陣列或服務管理員|安裝、啟用與設定服務和應用程式。<br /><br /> 使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板與檢視管理報表。|  
|完整控制|啟用網站集合層級的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能整合。<br /><br /> 建立 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫。<br /><br /> 建立資料摘要庫。|  
|參與|加入、編輯、刪除與下載 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿。<br /><br /> 設定資料重新整理。<br /><br /> 根據 SharePoint 網站上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿，建立新的活頁簿和報表。<br /><br /> 在資料摘要庫中建立資料服務文件|  
|讀取|將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿做為外部資料來源來存取，其中活頁簿 URL 是在連接對話方塊 (例如，在 Excel 的資料連接精靈) 中明確輸入的。|  
|僅檢視|檢視 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿。<br /><br /> 檢視資料重新整理記錄。<br /><br /> 將本機活頁簿連接至 SharePoint 網站上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿，以其他方式重新訂定其資料用途。<br /><br /> 下載活頁簿的快照集。 此快照集是資料的靜態複本，不包含交叉分析篩選器、篩選、公式或資料連接。 此快照集的內容類似於從瀏覽器視窗中複製資料格值。|  
  
##  <a name="excel"></a> PowerPivot 活頁簿的 Excel Services 安全性考量  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器端查詢處理與 Excel Services 緊密結合。 產品整合開始於文件層級，在此層級中， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿是包含或參考 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的 Excel 活頁簿 (.xlsx) 檔案。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿沒有個別的副檔名。  
  
 在 SharePoint 網站上開啟 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿時，Excel Services 會讀取內嵌的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料連接字串，並將要求轉送至本機 SQL Server Analysis Services OLE DB 提供者。 接著，此提供者會將連接資訊傳遞到伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器。 若要讓要求在兩部伺服器間順暢地流動，必須將 Excel Services 設定為使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 所需的設定。  
  
 在 Excel Services 中，您可以針對信任的位置、信任的資料提供者以及信任的資料連線庫指定安全性相關的組態設定。 下表將描述啟用或強化 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料存取的設定。 如果有設定未列在此處，對 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器連接並沒有影響。 如需如何逐步指定這些設定的指示，請參閱 [初始組態 (PowerPivot for SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)中的＜啟用 Excel Services＞一節。  
  
> [!NOTE]  
>  與安全性最相關的設定會套用至信任的位置。 如果您要保留預設值或在不同的網站使用不同的值，您可以針對包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的網站建立其他信任的位置，然後只針對該網站進行下列設定。 如需詳細資訊，請參閱 [在管理中心建立 Power Pivot 網站的信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
|區域|設定|Description|  
|----------|-------------|-----------------|  
|Web 應用程式|Windows 驗證提供者|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 會將它從 Excel Services 取得的宣告 Token 轉換為 Windows 使用者識別。 將 Excel Services 當做資源使用的所有 Web 應用程式都必須設定為使用 Windows 驗證提供者。|  
|信任的位置|位置類型|此值必須設為 **[Microsoft SharePoint Foundation]**。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器會擷取 .xlsx 檔案的複本，並將其載入伺服陣列中的 Analysis Services 伺服器。 伺服器只能從內容庫擷取 .xlsx 檔。|  
||允許外部資料|此值必須設為 **[信任的資料連線庫與內嵌連線]**。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料連接內嵌在活頁簿中。 如果您不允許內嵌連接，使用者可以檢視 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 快取，但是他們將無法與 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料進行互動。|  
||重新整理時警告|如果您要使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫儲存活頁簿與報表，應該停用此值。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫包含文件預覽功能，開啟時重新整理與重新整理時警告同時關閉時效果最好。|  
|信任的資料提供者|MSOLAP.4<br /><br /> MSOLAP.5|預設隨附 MSOLAP.4，但是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料存取需要 MSOLAP.4 提供者為 SQL Server 2008 R2 版。<br /><br /> MSOLAP.5 會隨 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] for SharePoint 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 版安裝。<br /><br /> 請不要從信任的資料提供者清單中移除這些提供者。 在某些情況下，您可能需要在伺服器陣列中的其他 SharePoint 伺服器上，安裝此提供者的額外複本。 如需詳細資訊，請參閱＜ [Install the Analysis Services OLE DB Provider on SharePoint Servers](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)＞。|  
|信任的資料連線庫|選擇性。|您可以使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿中的 Office 資料連接 (.odc) 檔案。 如果您使用 .odc 檔案來提供本機 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的連接資訊，就可以將相同的 .odc 檔案加入至這個連線庫。|  
|使用者定義函數組件|不適用。|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 會忽略您為 Excel Services 建立部署的使用者定義函數組件。 如果您依賴使用者定義的組件執行特定行為，請注意 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查詢處理不會使用您建立的使用者定義函數。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 Power Pivot 服務帳戶](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [設定 Powerpivot 無人看管的資料重新整理帳戶 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)   
 [在管理中心建立 Power Pivot 網站的信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Powerpivot 安全性架構](http://go.microsoft.com/fwlink/?linkID=220970)  
  
  
