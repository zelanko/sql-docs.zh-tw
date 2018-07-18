---
title: 鑽研、 向下鑽研、 子報表和巢狀的資料區域 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4791a157-b028-4698-905d-f1dd0887aa0d
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 4a951ab61a50ddf9983678a50989e5560d40f85e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228828"
---
# <a name="drillthrough-drilldown-subreports-and-nested-data-regions-report-builder-and-ssrs"></a>鑽研、向下鑽研、子報表和巢狀資料區 (報表產生器及 SSRS)
  您可以利用各種不同的方式來組織資料，以顯示總結資料與詳細資料之間的關聯性。  您可以將所有資料放入報表但設為隱藏，直到使用者按一下來顯示詳細資料；這是 *「向下鑽研」* (Drilldown) 動作。 您可以在資料區域 (例如資料表或圖表) 中顯示資料，再將這個資料區域放到另一個資料區域 (例如資料表或矩陣) 內，成為 *「巢狀」* (Nested) 結構。 您可以在 *「子報表」* (Subreport) 中顯示資料，此報表完全包含在主報表內。 或者，您可以將詳細資料放到 *「鑽研」* (Drillthrough) 報表，這是當使用者按一下連結時另外顯示的報表。  
  
 ![rs_DrillThruDrilldownEtc](../media/rs-drillthrudrilldownetc.gif "rs_DrillThruDrilldownEtc")  
  
 A. 鑽研報表  
  
 B. 「子報表」  
  
 C. 巢狀資料區  
  
 D. 向下鑽研動作  
  
 上述所有項目均有共通點，但用途不同，功能也不同。 其中的鑽研報表和子報表實際上是獨立報表。 巢狀是將一個資料區域放到另一個資料區域的方式。 向下鑽研是可以套用到任何報表項目的動作，以隱藏和顯示其他報表項目。 您可以透過上述所有方式來組織和顯示資料，以協助使用者更進一步了解您的報表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SummaryCharacteristics"></a> 特性摘要  
 下表簡要地敘述這些不同特性。 稍後會在此主題另一節說明細節。 比較內容不含向下鑽研，因為您可以將它的顯示和隱藏動作套用到任何報表項目。  
  
|特徵|子報表|「鑽研」|「巢狀」|  
|-----------|---------------|------------------|------------|  
|使用主報表的資料集|相同或相異|相同或相異|相同|  
|擷取資料|與主報表同時擷取資料|一次擷取一份鑽研報表的資料|與主報表同時擷取所有資料|  
|是否處理和轉譯|隨主報表|按一下連結時|隨主報表。|  
|執行|較慢 (但隨主報表擷取所有資料)|較快 (但不會隨主報表擷取所有資料)|較快 (且隨主報表擷取所有資料)|  
|使用參數|是|是|否|  
|可以重複使用|做為其他報表中的報表、子報表或鑽研報表|做為其他報表中的報表、子報表或鑽研報表|無法重複使用。|  
|位置|主報表外部，相同或不同的報表伺服器|主報表外部，相同的報表伺服器|主報表內部|  
|顯示|在主報表|在不同報表|在主報表|  
  

  
##  <a name="Details"></a> 特性詳細說明  
  
###  <a name="Datasets"></a> 使用的資料集  
 子報表和鑽研報表可以使用主報表的相同資料集，也可以使用不同的資料集。 巢狀資料區域使用相同的資料集。  
  
###  <a name="RetrieveData"></a> 擷取資料  
 子報表和巢狀資料區域與主報表同時擷取資料。 鑽研報表則否。 鑽研報表會在使用者按一下連結時擷取資料。 如果必須同時擷取主報表和從屬報表的資料，這就值得注意。  
  
###  <a name="ProcessRender"></a> 處理與轉譯  
 子報表會當做主報表的一部分來處理。 例如，如果顯示訂單詳細資訊的子報表加入到詳細資料列的資料表資料格中，則資料表的每一個資料列會處理子報表一次，並將子報表當做主報表的一部分來轉譯。 只有當使用者按一下摘要主報表內的鑽研連結時，才會處理及轉譯鑽研報表。  
  
###  <a name="Performance"></a> 效能  
 在決定使用哪一項時，可以考慮使用資料區域代替子報表，尤其是如果子報表並非由多個報表使用。 這是因為報表伺服器會將子報表的每一個執行個體，都視為獨立的報表來處理，所以可能會影響效能。 資料區與子報表的功能和彈性相同，但效能更佳。 鑽研報表的效能也比子報表好，因為這種報表不會與主報表同時擷取所有資料。  
  
###  <a name="Parameters"></a> 使用參數  
 鑽研報表和子報表通常具有指定要顯示什麼報表資料的報表參數。 例如，當您在主報表中按一下銷售訂單號碼時，鑽研報表隨即開啟 (接受銷售訂單號碼當做參數)，然後顯示該銷售訂單的所有資料。 在主報表中建立連結時，會指定要當做參數而傳遞至鑽研報表的值。  
  
 若要建立鑽研報表或子報表，您必須先設計目標鑽研報表或子報表，然後再建立鑽研動作或將參考加入至主報表。  
  
###  <a name="Reusability"></a> 重複使用性  
 子報表和鑽研報表是獨立的報表， 因此可以用於多份報表或顯示為獨立報表。 巢狀資料區域不可重複使用。 您無法將它們儲存成報表組件，因為它們是內嵌在資料區域裡。 您可以將包含它們的資料區域儲存成報表組件，但巢狀資料區域本身則不行。  
  
###  <a name="Location"></a> 位置  
 子報表和鑽研報表都是獨立報表，因此儲存在主報表外部。 子報表可以位於相同或不同的報表伺服器上，但鑽研報表必須位於相同的報表伺服器上。 巢狀資料區域屬於主報表的一部分。  
  
###  <a name="Display"></a> 顯示器  
 子報表和巢狀資料區域會顯示在主報表中。 鑽研報表則會另外獨立顯示。  
  

  
##  <a name="InThisSection"></a> 本節內容  
 [鑽研報表&#40;報表產生器及 SSRS&#41;](drillthrough-reports-report-builder-and-ssrs.md)  
 說明使用者按一下主報表中的連結時開啟的報表。  
  
 [子報表&#40;報表產生器及 SSRS&#41;](subreports-report-builder-and-ssrs.md)  
 說明顯示在主報表主體內的報表。  
  
 [巢狀資料區域&#40;報表產生器及 SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)  
 說明將某個資料區套疊在另一個資料區內，例如，套疊在矩陣內的圖表。  
  
 [向下鑽研動作&#40;報表產生器及 SSRS&#41;](drilldown-action-report-builder-and-ssrs.md)  
 說明如何使用向下鑽研動作隱藏和顯示報表項目。  
  
 [指定外部項目的路徑&#40;報表產生器及 SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)  
 說明如何參考報表定義檔案外部的項目。  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)  
  
  
