---
title: 使用鑽研結構資料 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a693979c-0564-4d6d-b35d-cbbc8f350469
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 68d5d29a4aed7380bd7a53c65d140aac24912392
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745539"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>在結構資料上使用鑽研 (基本資料採礦教學課程)
  做為其廣告宣傳活動中，一部分[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]傳送郵件給潛在客戶在 34 到 40 歲人口統計。 行銷部門決定，他們也想要傳送郵件給五年以前曾經從 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 購買自行車的客戶。 在這一課，您將會識別擁有比較舊的自行車的客戶，並擷取他們的連絡資訊。 此資訊不包括在模型中，但是會包括在結構中。 若要擷取連絡資訊，您要先確定此結構已啟用鑽研，然後您將會使用鑽研來顯示目標客戶的姓名和地址。  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>針對採礦模型啟用鑽研  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，請在**Mining Models**  索引標籤的資料採礦設計師中，以滑鼠右鍵按一下**TM_Decision_Tree**模型，然後選取**屬性**。  
  
2.  在 [屬性] 視窗中，按一下 **[AllowDrillThrough]** ，然後選取 **[True]** 。  
  
3.  採礦模型索引標籤中，以滑鼠右鍵按一下模型，然後選取**處理序模型**。  
  
 如需詳細資訊，請參閱 <<c0> [ 鑽研查詢&#40;資料採礦&#41;</c0>](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>若要檢視採礦模型中的鑽研資料  
  
1.  在資料採礦設計師中，按一下 **[採礦模型檢視器]** 索引標籤。  
  
2.  選取  **TM_Decision_Tree**模型從**採礦模型**清單。  
  
3.  變更**背景**值`1`。 這樣就只會顯示模型中與購買自行車的客戶相關的部分。  
  
4.  從 **[檢視器]** 清單中，選取 [Microsoft 樹狀檢視器]。 這樣會強制檢視器重新整理並顯示新的篩選條件。 然後，找出**Age > = 34 和 < 41**節點並以滑鼠右鍵按一下節點。  
  
5.  選取 **[鑽研]** ，然後選取 **[模型和結構資料行]** ，開啟 **[鑽研]** 視窗。  
  
6.  捲動到 **[Structure.Date First Purchase]** 資料行，檢視較舊的自行車的購買日期。  
  
7.  若要將資料複製到剪貼簿，請以滑鼠右鍵按一下資料表中的任何資料列，然後選取 [全部複製]  。  
  
 恭喜！您已順利完成基本資料採礦教學課程。 現在您可以輕鬆地使用資料採礦工具，我們建議您最好也完成中繼資料採礦教學課程，其中會示範如何建立模型以供預測、購物籃分析和時序群集。  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [建立預測 &#40;資料採礦基本教學課程&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用預測查詢產生器來建立預測查詢](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
