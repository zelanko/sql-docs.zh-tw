---
title: 建立資料來源視圖（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac7730e8437eaed304ed69c40e45fc93ee9b5531
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68888642"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>建立資料來源檢視 (基本資料採礦教學課程)
  資料來源檢視建立在資料來源之上，而且會定義一個資料子集，然後您可以在採礦結構中使用該資料子集。 您也可以使用資料來源檢視加入資料行、建立導出資料行與彙總，以及加入具名檢視。 您可以使用資料來源檢視，在不修改原始資料來源的情況下，選取與專案相關的資料、建立資料表之間的關聯性，以及修改資料的結構。 如需詳細資訊，請參閱 [多維度模型中的資料來源檢視](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)。  
  
### <a name="to-create-a-data-source-view"></a>若要建立資料來源檢視  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 [**資料來源視圖**]，然後選取 [**新增資料來源視圖**]。  
  
2.  在 [歡迎使用資料來源檢視精靈]**** 頁面上，按 [下一步]****。  
  
3.  在 [**選取資料來源**] 頁面的 [**關聯式資料來源**] 底下，選取您在上一個工作中建立的 [艾德公司 DW 2012] 資料來源。 按 [下一步]  。  
  
    > [!NOTE]  
    >  如果您想要建立資料來源，請以滑鼠右鍵按一下 [**資料來源**]，然後按一下 [**新增資料來源**]，以啟動 [資料來源嚮導]。  
  
4.  在 [**選取資料表和資料檢視]** 頁面上，選取下列物件，然後按一下向右箭號，將它們包含在 [新資料來源] 視圖中：  
  
    -   **ProspectiveBuyer （dbo）** -潛在自行車購買者的資料表  
  
    -   **vTargetMail （dbo）** -查看過去自行車購買者的歷程記錄資料  
  
5.  按 [下一步]  。  
  
6.  根據預設，在 [**正在完成嚮導]** 頁面上，[資料來源] 視圖的名稱為 [艾德作品] [DW 2012]。 將 [名稱] `Targeted Mailing`變更為，然後按一下 **[完成]**。  
  
     新的 [資料來源] 視圖隨即在 **[目標郵寄] [Design]** ] 索引標籤中開啟。  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [建立資料來源 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一課  
 [第2課：建立目標郵寄結構 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [定義資料來源視圖 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services)  
  
  
