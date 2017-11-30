---
title: "報表產生器中的報表組件和資料集 | Microsoft Docs"
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
caps.latest.revision: "9"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a22f1e59a693551ffb1575ffdeb351c58480b96b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="report-parts-and-datasets-in-report-builder"></a>報表產生器中的報表組件和資料集
  在報表產生器中，在報表內包含資料最簡單的方式，就是從報表組件庫加入報表組件。 報表組件包含相依的資料集，稱為 *「相依資料集」*(Dependent Dataset)。 相依資料集是以共用資料來源為基礎，而且可以是內嵌資料集或共用資料集。 深入了解 [報表組件](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
 在報表內包含資料的另一個方式是使用共用資料集。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)(Dependent Dataset)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Adding"></a> 將包含相依資料集的報表組件加入至您的報表  
 當您將報表組件加入至報表時，其中包含的相依資料集也會加入到報表中。 報表組件可能包含其中內含許多其他報表項目的矩形，因此，它可以將多個相依資料集加入至報表中。 每個共用資料集都是一個獨立的參考；其相依的共用資料來源不會加入到您的報表中。 每個內嵌資料集也會加入相依的內嵌或共用資料來源。  
  
 內嵌資料來源的認證不會儲存為報表組件的一部分。 如果將內嵌資料來源加入到您的報表，系統會在您執行報表時提示您提供認證。 為避免系統提示您提供認證，請搭配預存認證使用以共用資料來源為基礎的報表組件。  
  
 將報表組件加入至報表之後，加入的資料集就與您建立的內嵌或共用資料集沒什麼不同了。 您可以在 [報表資料] 窗格中，檢視額外的資料集。 內嵌資料集會出現在對應的共用資料來源下方，而共用資料集則出現在 [共用資料集] 資料夾的下方。  
  
##  <a name="Customizing"></a> 自訂相依資料集  
 將報表組件加入至報表之後，您可以進行預覽，並決定是否要對資料進行一些變更。 您可以變更的內容取決於您要使用的資料集類型。  
  
 若要變更內嵌資料集的資料和資料選項，您可以編輯包括查詢在內的資料集屬性，就像您先前自己建立資料集一樣。  
  
 若要變更共用資料集的資料及資料選項，您僅能在您有足夠權限的報表伺服器上，變更共用資料集定義。 您也可以在報表中加入篩選、加入導出欄位，以及變更區分大小寫之類的資料選項，藉以自訂共用資料集的執行個體。 如需詳細資訊，請參閱[內嵌和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)。  
  
 如需如何變更共用資料集定義，或如何顯示報表中共用資料集之最新資料變更的詳細資訊，請參閱[建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) 和[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
##  <a name="Publishing"></a> 將相依資料集當做共用資料集發行  
 當您發行包含相依資料集的報表項目時，您可以選擇將每個資料集當做共用資料集發行，或當做仍然內嵌在報表項目中的內嵌資料集發行。  
  
 當您選取共用資料集選項時，資料集會儲存至報表伺服器，做為共用資料集定義。 在您的報表中，使用該資料集的每個報表項目都會進行更新，以指向現在位於報表伺服器上的共用資料集。 因此會發生兩件事：  
  
1.  在 [發行] 對話方塊中，已經發行的每個共用資料集都會從可用於發行之項目的清單中移除。  
  
2.  當您結束報表產生器，或啟動新的報表時，系統會提示您儲存報表。 如果您不儲存報表，下次開啟此報表並發行報表項目時，您可能會發行相同資料集的新複本。 為避免將共用資料集的多個複本儲存至報表伺服器，建議您儲存報表。  
  
> [!IMPORTANT]  
>  為確保您和其他人可以繼續成功地使用共用資料集中的資料，您必須了解保護報表項目安全背後的原則。 如需詳細資訊，請參閱 [保護共用資料集項目的安全](../../reporting-services/security/secure-shared-dataset-items.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表設計檢視 &#40;報表產生器&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [安全性 &#40;報表產生器&#41;](../../reporting-services/report-builder/security-report-builder.md)   
 [報表組件 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
