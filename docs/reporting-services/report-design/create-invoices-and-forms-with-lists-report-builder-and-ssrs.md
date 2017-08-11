---
title: "建立發票和表單的清單 （報表產生器及 SSRS） |Microsoft 文件"
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
ms.assetid: c33231a5-b3a8-42e4-95bc-d05bdf2222f5
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: dcbc50e4c1bb576d4956b569dc7644d8e6f23abf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="create-invoices-and-forms-with-lists-report-builder-and-ssrs"></a>建立發票和表單的清單 (報表產生器及 SSRS)
  清單資料區域會隨 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表資料集中的每一個群組或資料列重複。 清單可以用於建立自由形式的報表或表單 (如發票)，也可以與其他資料區域一起使用。 您可以定義包含任何數目之報表項目的清單。 清單可以是巢狀 WIT  
  
 若要快速地開始使用清單，請參閱[教學課程：建立自由格式報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-creating-a-free-form-report-report-builder.md)。  
  
> [!NOTE]  
>  您可以將清單當做報表組件，與報表分開發行。 請深入了解 [報表組件 (報表產生器及 SSRS)](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
##  <a name="AddingList"></a> 將清單加入報表  
 將清單從功能區上的 [插入] 索引標籤加入至設計介面。 根據預設，清單一開始在與詳細資料群組相關聯的資料列中有一個單一資料格。  
  
 ![在設計介面上的新清單報表項目](../../reporting-services/report-design/media/rs-listtemplatenew.gif "設計介面上的新清單報表項目")  
  
 當您在設計介面上選取清單時，資料列和資料行控點隨即出現，如下圖所示。  
  
 ![從 [工具箱] 中，選取加入新清單](../../reporting-services/report-design/media/rs-listtemplatenewselected.gif "新清單從工具箱新增選取")  
  
 您開始使用的清單是以 Tablix 資料區域為基礎的範本。 加入清單後，您可以透過指定篩選、排序或群組運算式來變更清單的內容或外觀，或變更清單跨報表頁面顯示的方式，藉以繼續增強設計。 如需詳細資訊，請參閱[控制報表頁面上的 Tablix 資料區顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)。 雖然清單以單一資料行和資料列開始，但是您可以加入巢狀或相鄰的資料列群組或資料行群組，或加入其他詳細資料列，以便進一步繼續開發您的清單設計。 如需詳細資訊，請參閱[探索 Tablix 資料區的彈性 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)。  
  
  
##  <a name="DisplayingLayout"></a> 以自由形式的配置顯示資料  
 若要以自由形式配置而非方格組織報表資料，您可以將清單加入到設計介面中。 將欄位從 [報表資料] 窗格拖曳至資料格。 根據預設，資料格包含當做容器使用的矩形。 在容器中移動每個欄位，直到擁有所需的設計為止。 當您在矩形容器中拖曳文字方塊時使用對齊線可協助您以垂直和水平方式對齊邊緣。 調整資料格的大小來移除不想要的空白字元。 如需詳細資訊，請參閱[變更資料列高度或資料行寬度 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-row-height-or-column-width-report-builder-and-ssrs.md)。  
  
 下圖顯示的清單可顯示有關順序的資訊，包括以下欄位：Date、Order、Qty、Product、LineTotal 和影像。  
  
 ![在 [設計] 檢視中、 4 個欄位及影像清單](../../reporting-services/report-design/media/rs-basiclistformdesign.gif "中設計 檢視中、 4 個欄位及影像清單")  
  
 在預覽中，清單會重複以顯示自由形式格式的欄位資料，如下圖所示：  
  
 ![預覽具有 4 個欄位和一個影像清單](../../reporting-services/report-design/media/rs-basiclistformpreview.gif "預覽具有 4 個欄位和一個影像清單")  
  
> [!NOTE]  
>  顯示在這些圖表中的虛線也包含在內，以顯示每個欄位值的自由形式配置。 在實際報表中通常不會使用虛線。  
  
  
##  <a name="DisplayingGrouping"></a> 利用一個群組層級顯示資料  
 清單會自動提供容器，因此您可以使用清單來顯示包含多個檢視的群組資料。 若要變更預設清單來指定群組，請編輯詳細資料群組、指定一個新名稱，並指定一個群組運算式。  
  
 例如，您可以內嵌顯示相同資料集之不同檢視的資料表和圖表。 您可以將群組加入到清單中，讓巢狀報表項目針對每個群組值重複一次。 下圖顯示依產品類別目錄分組的清單。 請注意，其中沒有詳細資料列， 而有兩個資料表以巢狀方式，並排在清單中。 第一個資料表會顯示包含總銷售額的子類別目錄。 第二個資料表則顯示依地理區域分組的類別目錄，其中包含一個顯示子類別目錄分佈的圖表。  
  
 ![具有 2 個資料表的清單，另一個巢狀圖表](../../reporting-services/report-design/media/rs-basiclistgroupdesign.gif "具有 2 個資料表，其中具有巢狀圖表的清單")  
  
 在預覽中，資料表會顯示自行車所有子類別目錄的總銷售額，而該資料表內部的資料表則顯示每個地理區域的銷售額明細。 透過使用運算式來指定總計的背景色彩與圖表的自訂調色盤，第一個資料表也提供圖表色彩的圖例。  
  
 ![預覽、 2 個資料表，其中具有巢狀圖表](../../reporting-services/report-design/media/rs-basiclistgrouppreview.gif "預覽，2 個資料表，其中具有巢狀圖表")  
  
  
## <a name="see-also"></a>另請參閱  
 [彙總函式參考 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [運算式範例 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
