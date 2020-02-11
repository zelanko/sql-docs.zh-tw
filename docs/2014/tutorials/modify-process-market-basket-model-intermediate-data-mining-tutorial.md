---
title: 修改和處理購物籃模型（元資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4987e3497b7d52ff11f8f52bc403105340f7f508
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63301366"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>修改及處理購物籃模型 (中繼資料採礦教學課程)
  在處理您建立的關聯性採礦模型之前，您必須變更兩個參數的預設值： [*支援* *] 和 [* 機率]。  
  
-   *支援*定義規則在被視為有效之前必須存在的案例百分比。 您將會指定，至少必須在百分之 1 的案例中找到規則。  
  
-   機率定義關聯在被視為有效之前*的可能性。* 您將會考量機率至少百分之 10 的任何關聯。  
  
 如需增加或減少支援和機率之影響的詳細資訊，請參閱[Microsoft 關聯分析演算法技術參考](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
 定義**關聯**性採礦模型的結構和參數之後，您將會處理此模型。  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>若要調整關聯模型的參數  
  
1.  開啟資料採礦設計師的 [**採礦模型**] 索引標籤。  
  
2.  在設計工具中，以滑鼠右鍵按一下方格中的 [**關聯**] 資料行，然後選取 **[設定演算法參數] 以開啟 [演算法參數**] 對話方塊。  
  
3.  在 [**演算法參數**] 對話方塊的 [**值**] 資料行中，設定下列參數：  
  
     MINIMUM_PROBABILITY = 0.1   
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>若要處理採礦模型  
  
1.  在的 [**採礦模型**] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]功能表上，選取 [**處理採礦結構] 和 [所有模型]。**  
  
2.  在詢問您是否要建立及部署專案的警告中，按一下 [**是]**。  
  
     [**進程採礦結構-關聯**] 對話方塊隨即開啟。  
  
3.  按一下 **[執行]** 。  
  
     [**處理進度**] 對話方塊隨即開啟，以顯示模型處理的相關資訊。 處理新的結構和模型可能需要花一些時間。  
  
4.  處理完成之後，按一下 [**關閉**] 以結束 [**處理進度**] 對話方塊。  
  
5.  再按一次 [關閉]，**結束**[**處理常式採礦結構-關聯**] 對話方塊。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [流覽購物籃模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;資料採礦&#41;的處理需求和考慮](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
