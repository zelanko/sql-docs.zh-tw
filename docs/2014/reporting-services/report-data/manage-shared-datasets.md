---
title: 管理共用資料集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2cbb1fa3-959e-4df6-9887-ebc93cc1b686
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: af52516dccd163380cc6c36be9d0a862f3de94e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37168299"
---
# <a name="manage-shared-datasets"></a>管理共用資料集
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，共用資料集是從連接至外部資料來源的共用資料來源擷取資料。 共用資料集提供方法以共用查詢，可協助您為多個報表提供一致的資料集。 資料集查詢可以包含資料集參數。 您可以在第一次使用時或指定排程，設定共用資料集以快取特定參數組合的查詢結果。 您可以使用共用資料集快取，配合報表快取及報表資料摘要，協助管理資料來源的存取。  
  
 共用資料集只使用共用資料來源，而不使用內嵌資料來源。 共用資料集可以根據已支援 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料延伸模組或報表模型的任何資料來源。  
  
## <a name="creating-and-using-shared-datasets"></a>建立及使用共用資料集  
 若要建立共用資料集，您必須使用可建立共用資料集定義檔 (.rsd) 的應用程式。 您可以使用下列其中一個應用程式來建立共用資料集：  
  
-   報表產生器：使用共用資料集設計模式，並將共用資料集儲存至報表伺服器或 SharePoint 網站。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的報表設計師：在 [方案總管] 中的 [共用資料集] 資料夾下建立共用資料集。 若要發行共用資料集，則將資料集部署到報表伺服器或 SharePoint 網站。  
  
-   上傳共用資料集定義 (.rsd) 檔案：您可以將檔案上傳至報表伺服器或 SharePoint 網站。 在 SharePoint 網站上， 共用資料集進行快取或在報表中使用之前，上傳的檔案不會依結構描述進行驗證。  
  
 共用資料集定義包括：查詢、含預設值的資料集參數、資料選項 (例如，大小寫區分和資料集篩選)。 只要報表中包含共用資料集，就會使用您在定義中設定的值。  
  
 若要在報表中使用共用資料集，您可以開啟應用程式 (如報表產生器)，瀏覽至報表伺服器或 SharePoint 網站，然後選取共用資料集。 這會將共用資料集的執行個體加入報表。 您無法在報表中檢視或者變更查詢或共用資料集的共用資料來源。 您可以指定套用至報表中執行個體的其他資料集屬性值集。 例如，您可以加入篩選器，或變更區分大小寫等資料選項。 如需詳細資訊，請參閱 msdn.microsoft.com 上[報表產生器文件](http://go.microsoft.com/fwlink/?LinkId=154494)中的[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="managing-shared-datasets"></a>管理共用資料集  
 若要管理已發行共用資料集的屬性，您可以針對原生模式報表伺服器使用報表管理員，或是如果將報表伺服器部署為 SharePoint 整合模式，則使用 SharePoint 網站上的應用程式頁面。 您可以在共用資料集上執行的工作取決於您的角色指派及站台層級和項目層級使用權限，如果實際上權限是繼承而來的，則也包括資料夾權限。 共用資料集的項目層級安全性遵循與報表相同的項目層級安全性模型。 如需詳細資訊，請參閱 [保護共用資料集項目的安全](../security/secure-shared-dataset-items.md)。  
  
 您可以與使用共用資料集的報表或其相依的共用資料來源分開，獨立管理共用資料集項目屬性 (包括所要使用的共用資料來源)。 若要變更查詢或屬於共用資料集定義一部分的其他資料集屬性，您必須編輯定義。  
  
### <a name="manage-shared-dataset-item-properties"></a>管理共用資料集項目屬性  
 下表列出您可以為共用資料集項目變更的項目屬性。  
  
|||  
|-|-|  
|編輯名稱|變更共用資料集的名稱。 相依項目的所有參考都將繼續運作。|  
|編輯描述|變更共用資料集的描述。|  
|編輯查詢執行逾時|設定查詢執行逾時，以秒為單位。 零 (0) 秒表示無逾時。決定資料集查詢逾時之前的秒數。若要指定無逾時值，請使用 0。 如需詳細資訊，請參閱[設定報表和共用資料集處理的逾時值 &#40;SSRS&#41;](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)。|  
|檢視相依項目|檢視使用此共用資料集的項目：已發行的報表組件、共用資料來源和報表。|  
  
 下列的其他共用資料集屬性會自動進行設定：  
  
|屬性|描述|  
|--------------|-----------------|  
|HasDataSourceCredentials|關聯的共用資料來源是否有認證儲存在報表伺服器上。|  
|HasUserProfileDependencies|報表在其查詢或篩選運算式中是否具有使用者全域集合參考。|  
  
## <a name="viewing-or-changing-the-shared-dataset-definition"></a>檢視或變更共用資料集定義  
 共用資料集屬性 (包括查詢、資料集參數、預設值、資料集篩選，以及定序和大小寫區分等資料選項) 是儲存於共用資料集定義中。 如果您具有足夠的權限，便可檢視與變更定義。  
  
 若要檢視或變更共用資料集定義，請在共用資料集設計模型中的報表產生器之類應用程式中，編輯共用資料集。 變更之後，將共用資料集定義回存至伺服器或網站。  
  
 在 XML 中檢視共用資料集定義的另一個方法是：在報表管理員中使用 URL 存取語法。 例如，若要檢視每個資料集參數的預設值，您可以使用下列 URL 存取命令，從報表伺服器顯示名為 DataSet1 的共用資料集定義：  
  
```  
http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
```  
  
## <a name="controlling-access-to-the-shared-dataset-definition"></a>控制共用的資料集定義的存取  
 根據預設，下列工作適用於共用資料集上的作業。  
  
-   **檢視報表** ：檢視共用資料集項目和項目屬性。  
  
-   **取用報表** ：讀取共用資料集定義。  
  
-   **管理報表** ：建立及刪除共用資料集，並編輯共用資料集屬性。  
  
-   **在項目上設定安全性** ：檢視及修改共用資料集的安全性設定。  
  
 如需哪一個工作和權限控制存取原生模式報表伺服器上的資料來源屬性的詳細資訊，請參閱[保護共用資料集項目的](../security/secure-shared-dataset-items.md)。  
  
 檢視及編輯 SharePoint 文件庫內項目屬性的權限是由網站管理員所決定。 如需詳細資訊，請參閱 [報表伺服器項目的 SharePoint 網站和清單權限參考](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)。  
  
## <a name="how-to-work-with-shared-dataset-properties-on-a-report-server"></a>如何在報表伺服器上處理共用資料集屬性  
 您可以使用各種不同工具來處理共用資料集。 下表摘要列出方法和工具，並提供其他指示的連結。  
  
|工作|工具|連結|  
|----------|----------|----------|  
|新增共用資料集，或變更共用資料集定義屬性。|儲存在報表產生器中。<br /><br /> 部署在報表設計師中。<br /><br /> 上傳報表管理員中的 .rsd 檔案|msdn.microsoft.com 之[報表產生器文件](http://go.microsoft.com/fwlink/?LinkId=154494)中的[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。<br /><br /> [上傳檔案頁面&#40;報表管理員&#41;](../upload-file-page-report-manager.md)<br /><br /> 如果在相依的共用資料來源發行之前上傳共用資料集，必須以手動方式將共用資料集繫結至共用資料來源。 如需詳細資訊，請參閱 <<c0> [ 一般屬性頁面、 共用資料集&#40;報表管理員&#41;](../general-properties-page-shared-datasets-report-manager.md)。</c0>|  
|變更共用資料集項目屬性。|報表管理員|[一般屬性頁面、 共用資料集&#40;報表管理員&#41;](../general-properties-page-shared-datasets-report-manager.md)|  
|為報表中的共用資料集執行個體指定其他共用資料集屬性。|報表產生器報表設計師|[資料集屬性對話方塊，查詢](../dataset-properties-dialog-box-query.md)|  
|繫結至共用資料集的不同共用資料來源。|報表管理員|[資料來源選擇頁面&#40;報表管理員&#41;](../data-source-selection-page-report-manager.md)|  
|驗證資料集參數的預設值。|在報表產生器中開啟，或使用 URL 存取語法。|例如：<br /><br /> `http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
|啟用快取|報表管理員|[快取共用資料集&#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)<br /><br /> [快取頁面、 共用資料集&#40;報表管理員&#41;](../caching-page-shared-datasets-report-manager.md)|  
|建立或編輯快取重新整理計畫|報表管理員|[快取重新整理選項 &#40;報表管理員&#41;](../cache-refresh-options-report-manager.md)|  
|檢視共用資料集定義結構描述。|報表管理員|`http://<reportserver>/shareddatasetdefinition.xsd`|  
|在 SharePoint 整合模式中，同步處理報表伺服器與 SharePoint 網站之間的共用資料集定義|SharePoint 應用程式頁面|變更共用資料集項目屬性<br /><br /> 變更快取選項<br /><br /> 變更共用資料來源|  
  
## <a name="comparing-shared-datasets-with-other-report-server-items"></a>比較共用資料集與其他報表伺服器項目  
 在報表伺服器上管理多個項目類型時，了解這些項目與其他報表伺服器項目有何異同，會很有助益。  
  
 共用資料集以下列方式與共用資料來源和報表類似：  
  
-   共用資料集就像共用資料來源，是與使用的報表分開獨立管理。 在報表伺服器上管理共用資料集的一部分是能夠變更相依的共用資料來源，而不必編輯共用資料集定義。  
  
-   共用資料集也跟報表一樣，可以進行快取。 資料來源所需的認證必須符合快取的限制，而且必須為每個參數指定預設值。 如需詳細資訊，請參閱[快取共用資料集 &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)。  
  
-   跟報表一樣，每次發生處理時，就會使用報表伺服器上目前的項目定義。 如果變更共用資料集，使用該資料集的每個報表都會在處理報表時，使用報表伺服器上目前的定義。 如果已為共用資料集啟用快取，且變更共用資料集定義，則在快取中資料過期之前不會使用所做的變更。 您可以使用快取重新整理計劃，為多個報表提供一致的資料集。  
  
 共用資料集是以下列方式與已發行的報表組件相異：  
  
-   與已發行的報表組件不同的是，當報表在報表撰寫用戶端中開啟時，報表伺服器上共用資料集定義中的變更不會觸發更新通知。 當您執行報表時，會使用報表伺服器上目前共用資料集定義的資料。  
  
 共用資料集是以下列方式與訂閱類似：  
  
-   共用資料集可以使用快取的項目特定和共用排程。  
  
-   共用資料集遵循與訂閱相同的參數值指定規則。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器內容管理&#40;SSRS 原生模式&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [在原生模式報表伺服器上授與權限](../security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
