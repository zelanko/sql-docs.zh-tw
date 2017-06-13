---
title: "SharePoint 網站和清單權限參考報表伺服器項目 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
- permission sets [Reporting Services]
ms.assetid: 1fcb27bd-4c4a-43f4-bfff-e42a59c87c49
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca45a9fc4c37798983c4cc8956fbb27828a5ff01
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="sharepoint-site-and-list-permission-reference-for-report-server-items"></a>報表伺服器項目的 SharePoint 網站和清單權限參考
  本文中提供 SharePoint 權限的參考，可用來針對以 SharePoint 整合式模式執行的報表伺服器，授與報表伺服器作業的存取權。 如果您要建立自訂的權限等級，本主題可幫助您選擇適用的權限。  
  
 SharePoint 提供三十三種權限，可用來控制內容和作業的存取。 部分 (但非全部) 權限套用至涉及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器的文件和作業。 您可以使用本文中的權限參考表，找出支援特定報表工作的權限。  
  
 每份表格最開始先列出 SharePoint 權限和描述。 資料表中包括三個資料行，表示權限在預先定義的權限等級中使用的方式。 預先定義的權限等級包括下列各項：  
  
|權限等級|縮寫|  
|----------------------|------------------|  
|完整控制|**F**|  
|參與|**C**|  
|訪客|**V**|  
  
 不會影響報表伺服器的權限並不會列出。 所有個人化權限都會排除在此參考文件之外。 即使您可以將報表伺服器項目加入個人化的網站中，報表伺服器仍不會直接處理個人化要求或作業。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 &#124; SharePoint 2010 和 SharePoint 2013。|  
  
## <a name="list-permissions"></a>清單權限  
 您在包含報表伺服器項目的文件庫上設定的權限，會決定使用者存取這些項目的方式。  
  
|權限|說明|F|C|V|報表伺服器作業|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|管理清單|建立和刪除清單、新增或移除清單中的資料行，以及新增或移除清單的公用檢視。|X|||在從編輯工具發行作業期間，於 SharePoint 程式庫中建立資料夾。 此權限同時為管理報表記錄所需。|  
|加入項目|將項目新增至清單、將文件新增至文件庫，以及新增網頁討論區註解。|X|X||將報表、報表模型、共用資料來源，以及資源 (外部影像檔) 加入 SharePoint 程式庫。 建立共用資料來源。 從共用資料來源產生報表模型。 啟動報表產生器，並建立新報表或將模型載入報表產生器。|  
|編輯項目|編輯清單中的項目、編輯文件庫中的文件、編輯文件中的網頁討論區註解，以及在文件庫中自訂 Web 組件頁面。<br /><br /> 建立訂閱和編輯您建立的訂閱。|X|X||檢視過去的文件，包括報表記錄快照集。 編輯報表和其他文件的項目屬性。 設定報表處理選項。 設定報表上的參數。 編輯資料來源屬性。 建立報表記錄快照集。 在報表產生器中開啟報表模型或模型式報表，然後將變更儲存到檔案中。 指派點選連結報表至模型中的實體。 將報表定義、共用資料來源、報表模型或資源取代為更新的版本 (取代檔案，保留中繼資料)。 管理報表或模型中參考的相依項目。 自訂與特定報表相關的報表檢視器 Web 組件。<br /><br /> 建立、變更和刪除使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 傳遞延伸模組將報表傳遞至目標位置的訂閱。 只有訂閱擁有者和具有「管理警示」權限的使用者才能夠執行這些動作。|  
|刪除項目|刪除清單中的項目、文件庫中的文件，以及文件中的網頁討論區註解。|X|X||從程式庫中刪除報表、報表模型、共用資料來源，以及其他文件。|  
|檢視項目|檢視清單中的項目、文件庫中的文件，以及網頁討論區註解。|X|X|X|開啟報表、報表模型和其他文件，並且在報表伺服器上進行處理。|  
|開啟項目|使用伺服器端檔案處理常式檢視文件的來源。|X|X|X|檢視共用資料來源的清單。 下載報表定義或報表模型的來源檔案副本。 檢視使用報表模型做為資料來源的點選連結報表。|  
|檢視版本|檢視舊版的清單項目或文件。|X|X|X|檢視舊版的文件和報表快照集。|  
|刪除版本|刪除舊版的清單項目或文件。|X|X||刪除舊版的文件和報表快照集。|  
  
> [!NOTE]  
>  其他清單權限包括「覆寫取出」、「核准項目」及「檢視應用程式頁面」。 報表伺服器不會評估這些權限。 報表伺服器也不會處理這些作業。  
  
## <a name="site-permissions"></a>網站權限  
 網站權限決定並非與特定文件庫中所儲存項目直接相關之報表伺服器作業的存取。 例如，建立和管理共用排程 (可由多個文件庫中的項目使用)，以及設定報表檢視器網頁組件 (可在整個網站上使用)。  
  
|權限|說明|F|C|V|報表伺服器作業|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|管理權限|建立和變更網站上的權限等級，並且將權限指派給使用者和群組。|X|||您可以變更所有報表伺服器項目和作業的權限。 還可以設定模型項目的安全性。|  
|管理網站|執行所有網站管理工作，以及管理內容。|X|||建立、變更和刪除共用排程。|  
|加入和自訂頁面|加入、變更或刪除 HTML 頁面或網頁組件頁面，並且使用與 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]相容的編輯器編輯網站。|X|||新增或移除報表檢視器網頁組件。|  
|瀏覽使用者資訊|檢視有關網站使用者的資訊。|X|X|X|跨不同的網站、文件庫和資料夾瀏覽報表和其他項目。 將報表和其他項目發行到文件庫。|  
|列舉權限|列舉網站、清單、資料夾、文件或清單項目的權限。|X|||讀取所有報表伺服器項目的權限。 檢視使用內含模型項目安全性設定之報表模型的點選連結報表。|  
|管理警示|管理網站上所有使用者的警示。|X|||建立、變更和刪除網站上的任何訂閱。|  
|使用遠端介面|使用 SOAP、Web DAV 或 SharePoint Designer 介面存取網站。|X|X|X|用於呼叫報表伺服器的 URL Proxy 端點。|  
|開啟|開啟網站、清單或資料夾以存取該容器內的項目。|X|X|X|讀取排程和項目屬性。|  
  
## <a name="see-also"></a>請參閱＜  
 [Reporting Services to SharePoint Groups and Permissions 中比較角色和工作](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
