---
title: 在報表產生器中預覽報表 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ba6b5bdd-d8c6-4aa8-ba32-3a10b11969d4
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb6447d896a68a932e24223944fd6117f54638eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33022345"
---
# <a name="previewing-reports-in-report-builder"></a>在報表產生器中預覽報表
  當您建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表時，這對經常預覽報表以確認報表如預期般顯示相當有幫助。 若要預覽報表，按一下 **[執行]**。 報表隨即在預覽模式下呈現。  
  
 報表產生器會在連接到報表伺服器時使用編輯工作階段，藉以改善預覽經驗。 編輯工作階段會建立一個資料快取，並讓快取中的資料集可以進行重複的報表預覽。 編輯工作階段不是一個您可以直接互動的功能，但是，當您預覽報表並了解報表呈現速度為什麼較快或較慢時，了解何時重新整理快取的資料集將會協助您提升效能。  
  
 編輯工作階段的其他優點包括，能夠編輯使用內嵌資料來源或參考項目的報表，例如儲存在報表伺服器上的影像或子報表。  
  
> [!NOTE]  
> 在報表產生器中預覽與在瀏覽器中檢視有些不同。 例如，當您指定日期/時間類型參數時新增至報表的月曆控制項，在報表產生器中與在瀏覽器中會不同。 
  
## <a name="improving-preview-performance"></a>提升預覽效能  
 您建立和更新報表的方式會影響報表在預覽中呈現的速度。 當您第一次預覽依賴伺服器參考的報表時，系統會為您建立編輯工作階段，而且執行報表時所使用的資料會加入到儲存在報表伺服器上的資料快取中。 當您針對報表進行不會影響資料的變更時，報表會使用資料的快取副本。 也就是說，每次預覽報表時，您都看不到資料變更。 如果您想要新的資料，請按一下功能區上的 [重新整理] 按鈕。  
  
 下列動作會重新整理快取，並減慢您下次預覽報表的報表呈現速度：  
  
-   加入、變更或刪除資料集。 快取資料集包含報表所使用的所有資料集，而且對於任何資料集的修改都會讓快取資料集失效。 這包括變更資料集中的名稱、查詢或欄位。  
  
    > [!NOTE]  
    >  如果資料集中包含您預期不會使用的大量欄位，您應該考慮更新資料集來省略這些欄位。 雖然這樣會建立新的編輯工作階段，而且第一次預覽報表的速度會較慢，但是快取資料集較小有益於報表伺服器的整體效能。  
  
-   加入、變更或刪除資料來源。 這包含變更資料來源的名稱或屬性、資料來源的資料延伸模組，或是資料來源連接的屬性。  
  
-   將報表所使用的共用資料來源變更為不同的資料來源。  
  
-   變更報表的語言。  
  
-   變更報表所使用的組件或自訂程式碼。  
  
-   加入、變更或刪除報表或參數值中的查詢參數。  
  
 對於報表配置和資料格式所做的變更不會影響快取資料集。 您可以在不重新整理快取資料集的情況下執行下列動作：  
  
-   加入或移除資料區，例如資料表、矩陣或圖表。  
  
-   從報表加入或刪除資料行。 資料集中的所有欄位都可供報表中的使用者使用。 加入或移除報表中的欄位不會影響資料集。  
  
-   變更欄位在資料表和矩陣中的順序。  
  
-   加入、變更或刪除資料列和資料行群組。  
  
-   加入、變更或刪除資料值在欄位中的格式。  
  
-   加入、變更或刪除影像、線條或文字方塊。  
  
-   變更分頁符號。  
  
 第一次預覽報表時會建立編輯工作階段。 根據預設，編輯工作階段會持續 7200 秒 (2 小時)。 每次執行報表時，此工作階段會重設為 2 小時。 當編輯工作階段到期時，系統會刪除資料快取。 如果編輯工作階段到期，下次您預覽報表時，系統會再次自動建立一個。 編輯工作階段的到期時間可以設定。 如果您發現 2 小時太長或太短，請連絡報表伺服器的管理員。  
  
 根據預設，資料快取最多可以容納 5 個資料集。 如果您使用多個不同的參數值組合，報表可能需要更多資料。 這需要重新整理快取，而且當您下次預覽報表時，報表的呈現速度會更慢。 快取中的項目數可以由報表伺服器的管理員設定。  
  
## <a name="concurrency-of-report-updates"></a>報表更新並行  
 當您更新報表，並將其儲存到報表伺服器時，您會經常預覽它。 當您正在更新報表時，可能會有其他人正在進行更新，然後同時儲存該報表。 最後儲存的報表是可供未來檢視和更新的報表版本。 這表示，您預覽的報表版本可能不是再次開啟的版本。 您可以選擇使用 [報表產生器] 功能表上的 [另存新檔] 選項，將報表儲存成新的名稱。  
  
## <a name="external-report-items"></a>外部報表項目  
 您的報表可能包含的項目包括共用資料來源、外部影像，以及與報表個別儲存的子報表等等。 由於這些項目會個別儲存，因此可能會移到報表伺服器上的其他位置或是遭到刪除。 如果發生這個情況，您的報表可能無法預覽。 您可以更新報表以指出項目的更新位置；如果項目遭到刪除，則將其取代成現有的項目，或從報表中移除該項目的參考。  
  
 如果建立編輯工作階段之後，變更了您報表所使用的子報表，該報表將不會呈現在預覽中。 若要成功預覽報表，您應該儲存報表，或按一下 [重新整理] 來取得新的資料。  
  
## <a name="see-also"></a>另請參閱  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [儲存報表 &#40;報表產生器&#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)  
  
  
