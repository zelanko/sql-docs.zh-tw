---
title: 建立資料來源檢視 （基本資料採礦教學課程） |Microsoft Docs
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
ms.openlocfilehash: b11844e6b184099a9c6146d290a0dc081429f5d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273402"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>建立資料來源檢視 (基本資料採礦教學課程)
  資料來源檢視建立在資料來源之上，而且會定義一個資料子集，然後您可以在採礦結構中使用該資料子集。 您也可以使用資料來源檢視加入資料行、建立導出資料行與彙總，以及加入具名檢視。 您可以使用資料來源檢視，在不修改原始資料來源的情況下，選取與專案相關的資料、建立資料表之間的關聯性，以及修改資料的結構。 如需詳細資訊，請參閱 [多維度模型中的資料來源檢視](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
### <a name="to-create-a-data-source-view"></a>若要建立資料來源檢視  
  
1.  中**方案總管**，以滑鼠右鍵按一下**資料來源檢視**，然後選取**新增資料來源檢視**。  
  
2.  在 [歡迎使用資料來源檢視精靈] 頁面上，按一下 [下一步]。  
  
3.  在  **Zdroj Dat**頁面的 **關聯式資料來源**，選取您在前一項工作中建立的 Adventure Works DW 2012 資料來源。 按一下 [下一步] 。  
  
    > [!NOTE]  
    >  如果您想要建立資料來源，以滑鼠右鍵按一下**資料來源**，然後按一下**新的資料來源**來啟動資料來源精靈。  
  
4.  在 **選取資料表和檢視**頁面，選取下列物件，然後按一下向右箭號，將它們包含在新的資料來源檢視：  
  
    -   **ProspectiveBuyer (dbo)** -潛在自行車買主的資料表  
  
    -   **vTargetMail (dbo)** -有關過去自行車買主的歷程記錄資料檢視  
  
5.  按一下 [下一步] 。  
  
6.  在 [**完成精靈]** 頁面上，預設的資料來源檢視名為 Adventure Works DW 2012。 將名稱變更為`Targeted Mailing`，然後按一下**完成**。  
  
     在中開啟新的資料來源檢視**Targeted Mailing.dsv [設計]**  索引標籤。  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [建立資料來源&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：建立目標的郵寄結構&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [定義資料來源檢視 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md)  
  
  
