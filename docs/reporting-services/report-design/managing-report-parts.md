---
title: "管理報表組件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 41947b4c-8ecf-4e4f-b30e-66e1d6692b74
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 310cad57050dba44c5303b78ea33e5b3f42d309c
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="managing-report-parts"></a>管理報表組件
  報表組件可以由多個使用者在分頁報表中重複使用，也可以在多個報表中重複使用。 使用者可以搜尋伺服器上的報表組件，並將其加入至報表中。  使用者也可以收到伺服器上報表組件更新的通知，然後重新發行新版本的報表組件。 這些報表撰寫動作可能會受報表服務安全性權限影響及控制。  本主題會檢閱報表組件位於伺服器上之後的屬性和行為。  
  
## <a name="managing-report-parts"></a>管理報表組件  
 若要管理報表組件，您可以針對原生模式報表伺服器使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 入口網站，或是針對 SharePoint 整合模式報表伺服器使用應用程式頁面。  
  
### <a name="server-side-interaction-and-search"></a>伺服器端互動及搜尋  
 報表組件可以發行到原生模式或 SharePoint 整合模式的報表伺服器。 使用者可以使用報表撰寫應用程式 (如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 報表產生器) 中的報表組件庫功能，尋找報表組件並將其加入至報表中。 當使用者搜尋報表組件時，不管伺服器是以何種模式安裝，搜尋都會查看報表伺服器目錄。  
  
 當報表組件從報表撰寫應用程式 (如報表產生器) 發行至 SharePoint 整合模式的報表伺服器時，報表伺服器目錄也會更新，而且會從組件庫搜尋以準確反映新的或更新的報表組件。  
  
#### <a name="directly-uploading-report-parts-to-a-sharepoint-folder"></a>直接將報表組件上傳到 SharePoint 資料夾  
 如果報表組件是直接上傳到 SharePoint 文件資料夾 (而非從報表撰寫應用程式發行)，則報表伺服器目錄不會更新。 從報表組件庫搜尋就找不到上傳的報表組件。 若要讓 SharePoint 資料夾與報表伺服器目錄保持同步，您可以在 SharePoint 伺服器上啟用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 檔案同步處理功能。 如需詳細資訊，請參閱 [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)。  
  
 檔案也可以透過呼叫一些報表服務管理 API (如 GetProperties 和 SetProperties 等) 進行同步處理。  
  
### <a name="organizing-and-moving-report-parts"></a>組織及移動報表組件  
 您應該事先考慮並規劃您的團隊將如何使用並組織報表組件、共用資料集和共用資料來源。 雖然您可以稍後再移動報表組件，但可能會產生問題。  
  
#### <a name="native-mode-report-server"></a>原生模式報表伺服器  
 如果您將原生模式報表伺服器上的報表組件移到相同伺服器上的其他任何資料夾中，並不會影響報表撰寫應用程式搜尋或下載報表組件更新的功能。 這是因為伺服器會依賴唯一的 ComponentID。 但是，如果報表組件是移到使用者沒有權限的資料夾，則他們搜尋時就找不到該報表組件，而且在報表組件有更新時，他們的報表也不會接到通知。  
  
#### <a name="report-server-in-sharepoint-integrated-mode"></a>SharePoint 整合模式下的報表伺服器  
 將報表組件移到不同的文件庫或資料夾，其影響與直接上傳到 SharePoint 伺服器相同：報表伺服器目錄不會進行同步處理。 若要避免這個狀況，請在 SharePoint 伺服器上啟動報表伺服器檔案同步處理功能。  
  
 例外狀況是子資料夾。 搜尋永遠都會搜尋子資料夾，因此，如果以手動方式將報表組件移到子資料夾， 從報表組件庫中進行搜尋還是會找到該組件。  
  
### <a name="report-server-catalog-properties"></a>報表伺服器目錄屬性  
 下表描述現有報表伺服器目錄欄位與報表組件相關的方式，以及與加入至報表組件目錄之新欄位相關的方式。 這些會在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 入口網站和 SharePoint 文件庫中公開，也會在如報表產生器之類的報表撰寫應用程式中公開。  
  
 (*) 表示是此版本的新功能。  
  
|屬性|說明|報表組件<br /><br /> 組件庫搜尋準則|  
|--------------|-----------------|---------------------------------------------|  
|名稱|這是使用者可以在報表組件庫中搜尋的其中一個準則。|是|  
|說明|您可能會想要使用某種方式來組織報表組件名稱，讓使用者更容易在組件庫中找到組件。 例如，您可以搜尋以「銷售>>」開頭的描述，以尋找與銷售相關資料和簡報有關的所有報表組件。|是|  
|CreatedBy|將報表組件加入報表伺服器資料庫的使用者識別碼。 確切的格式視驗證方法而定。 例如，某些驗證方法會導致在 [CreatedBy] 和 [ModifiedBy] 欄位中顯示完整的網域\使用者名稱。|是|  
|CreationDate|原先建立報表組件的日期。<br /><br /> 這是使用者可以在報表組件庫中搜尋的其中一個準則。|是|  
|ModifiedBy|ModifiedBy 是上次修改報表組件之使用者的識別碼。|是|  
|ModifiedDate|上次在伺服器上修改報表組件的日期。<br /><br /> 這個欄位是做為邏輯的一部分，以判斷伺服器端是否有報表組件更新。 如需詳細資訊，請參閱本表格稍後的 ComponentID 描述。|是|  
|SubType (*)|SubType 是一個字串，表示要搜尋的報表組件種類，例如 "Tablix" 或 "Chart"。|是|  
|ComponentID (*)|ComponentID 是報表組件的唯一識別碼。 這是加入至目錄的新欄位，在伺服器端及報表撰寫應用程式 (如報表產生器) 都可以看到。<br /><br /> 此欄位是由用戶端應用程式用來檢查更伺服器是否有報表組件更新。 用戶端應用程式會搜尋搜尋伺服器中，位於目前用戶端報表的 ComponentID。 如果有相符的 ComponentID，就會將 ModifiedDate 與用戶端報表項目的 SyncDate 相比較。|N0|  
  
## <a name="controlling-access-to-report-parts"></a>控制報表組件的存取  
 下表描述預設角色指派，以及這些指派如何讓您執行各種作業。 角色指派名稱會依所使用之報表伺服器的類型而有所不同。  
  
### <a name="server-in-native-mode"></a>原生模式下的伺服器  
  
|動作|角色|  
|-------------|-----------|  
|加入、刪除、編輯項目屬性、管理安全性，以及下載報表組件|內容管理員<br /><br /> 我的報表|  
|加入、刪除及下載報表組件|發行者|  
|搜尋及重複使用|瀏覽器<br /><br /> 報表產生器|  
  
### <a name="server-in-sharepoint-integrated-mode"></a>SharePoint 整合模式下的伺服器  
  
|動作|角色|  
|-------------|----------|  
|加入、刪除、編輯項目屬性、管理安全性，以及下載報表組件|完整控制|  
|加入、刪除、編輯項目屬性，以及下載報表組件|設計<br /><br /> 參與|  
|搜尋及重複使用|讀取<br /><br /> 僅檢視|  
  
### <a name="security-considerations"></a>安全性考量  
  
-   在報表中重複使用報表組件定義時，它們會連同識別用的 ComponentID 整個複製到報表定義中。 如果伺服器上的報表組件更新，使用者可以選擇將更新的報表組件下載到其報表中。 更新也是報表組件的完整複本，取代其報表中現有版本的報表組件。  
  
    > [!IMPORTANT]  
    >  這些步驟中每一個步驟，都務必要確定報表組件都是在受信任位置及使用者的報表中重複使用。  
  
-   報表組件會使用與現有「資源」項目類型相同的權限原則。 在資料夾之中，傳統資源項目與來自安全性繼承檢視方塊的報表組件之間沒有差異。 報表組件會繼承與同一個資料夾中影像相同的權限原則。 需要區別這兩者時，可以為想要的報表組件設定項目層級安全性。 或者，您可以將報表組件放在與已設定之正確權限不同的資料夾中。  
  
## <a name="see-also"></a>請參閱＜  
 [報表產生器中的報表組件和資料集](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [疑難排解報表組件 (報表產生器及 SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [報表設計師中的報表組件 &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)  
  
  
