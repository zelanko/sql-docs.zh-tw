---
title: 鑽研報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 938a6450-67c1-4eef-80b4-8fdaefeed584
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63119bf6d8ba4e9d907b9c6cdfb6bfe0b7765941
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105936"
---
# <a name="drillthrough-reports-report-builder-and-ssrs"></a>鑽研報表 (報表產生器及 SSRS)
  鑽研報表是使用者從另一個報表按一下連結所開啟的報表。 鑽研報表通常包含有關原始摘要報表之項目的詳細資料。 例如，在此圖中，銷售摘要報表會列出銷售訂單和總計。 當使用者按一下摘要清單中的訂單號碼時，會開啟另一份含有訂單詳細資料的報表。  
  
 ![rs_DrillThru](../media/rs-drillthru.gif "rs_DrillThru")  
  
 在使用者按一下主報表中的連結，開啟鑽研報表之前，不會擷取鑽研報表中的資料。 如果必須同時擷取主報表和鑽研報表的資料，請考慮使用子報表。 如需詳細資訊，請參閱[子報表 &#40;報表產生器及 SSRS&#41;](subreports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  當您在報表產生器中工作時，必須連接至報表伺服器，才能檢視按一下主報表中的鑽研連結時，所開啟的鑽研報表。  
  
 若要快速地開始使用鑽研報表，請參閱[教學課程：建立鑽研及主報表 &#40;報表產生器&#41;](../tutorial-creating-drillthrough-and-main-reports-report-builder.md)。 在兩個商業智慧方案也配備了鑽研報表[BI 報表：報表和訂閱案例](https://technet.microsoft.com/bi/ff769487.aspx)和[企業儀表板：銷售解決方案](https://technet.microsoft.com/bi/ff643005.aspx)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="parameters-in-drillthrough-reports"></a>鑽研報表中的參數  
 鑽研報表通常包含由摘要報表傳遞給它的參數。 在銷售摘要報表範例中，摘要報表在資料表資料格內的文字方塊中包含 [OrderNumber] 欄位。 鑽研報表包含一個接受訂單號碼當做值的參數。 當您在文字方塊上針對 [OrderNumber] 設定鑽研報表連結時，也會將目標報表的參數設定為 [OrderNumber]。 當使用者按一下摘要報表中的訂單號碼時，目標詳細資料報表就會開啟，並顯示該訂單號碼的資訊。 若要檢視依據參數值自訂鑽研報表的相關指示，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md) 和[InScope 函式 &#40;報表產生器及 SSRS&#41;](report-builder-functions-inscope-function.md)。  
  
## <a name="designing-the-drillthrough-report"></a>設計鑽研報表  
 若要建立鑽研報表，您必須先設計鑽研報表，再建立主報表中的鑽研動作。  
  
 鑽研報表可以是任何報表。 一般而言，鑽研報表會根據主報表的連結，接受一個或多個參數以指定要顯示的資料。 例如，如果主報表的連結是針對銷售訂單定義的，則銷售訂單號碼就會傳遞至此鑽研報表。  
  
## <a name="creating-a-drillthrough-action-in-the-main-report"></a>在主報表中建立鑽研動作  
 您可以將鑽研連結加入至文字方塊 (包括資料表或矩陣的資料格中的文字)、影像、圖表、量測計，以及任何其他有 [動作] 屬性頁的報表項目。 如需詳細資訊，請參閱[在報表上新增鑽研動作 &#40;報表產生器和 SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)。  
  
 您可以在主報表中建立鑽研動作，做為報表動作或 URL 動作。 如果是報表動作，則鑽研報表必須存在於與主報表相同的報表伺服器上； 如果是 URL 動作，則報表必須存在於完整的 URL 位置。 您針對報表伺服器或與報表伺服器整合的 SharePoint 網站指定報表的方式可能有所不同。如果報表伺服器是在 SharePoint 整合模式中設定，則只支援 URL 動作。  
  
 如需詳細資訊，請參閱[在報表上加入鑽研動作 &#40;報表產生器及 SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) 和[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
## <a name="viewing-a-drillthrough-report"></a>檢視鑽研報表  
 若要在發行具有鑽研連結的摘要報表之後加以檢視，您必須確定鑽研報表位於與摘要報表相同的報表伺服器上。 在所有情況下，使用者都必須擁有鑽研報表的權限，才能進行檢視。  
  
## <a name="see-also"></a>另請參閱  
 [鑽研、向下鑽研、子報表和巢狀資料區 &#40;報表產生器及 SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
