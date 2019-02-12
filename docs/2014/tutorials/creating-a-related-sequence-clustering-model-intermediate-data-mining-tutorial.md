---
title: 建立相關的時序群集模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71db7ba5246e151bbca8a52972a2ba835b80ddb6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035109"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>建立相關的時序群集採礦模型 (中繼資料採礦教學課程)
  探索時序群集模型之後，您了解到 Region 或 Income 等其他屬性對於模型也有很大的影響。因此，若要進一步了解時序，您需要建立相關的時序群集模型，並移除與客戶人口統計有關的屬性。  
  
 在這項工作中，您將建立一個區域時序群集模型的副本，然後從模型中移除任何與時序無直接關聯的資料行。  
  
 新的模型所包含的資料行，與所依據之採礦模型的資料行完全相同。 不過，您不必從採礦結構移除資料行，只要指定新的採礦模型忽略資料行即可。  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>若要製作時序群集模型的副本  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，在 資料採礦設計師中，按一下 [**採礦模型**] 索引標籤。  
  
2.  以滑鼠右鍵按一下您想要複製，並選取的模型**新的採礦模型**。  
  
3.  在 **新的採礦模型** 對話方塊中，輸入模型名稱，然後選取 Microsoft `Sequence Clustering`。  
  
     本教學課程中，輸入 名稱`Sequence Clustering`。  
  
4.  按一下 [確定] 。  
  
### <a name="to-remove-columns-from-the-mining-model"></a>若要從採礦模型移除資料行  
  
1.  在 **採礦模型**索引標籤上，在名為 時序群集中，新模型的資料行中按一下資料列**Income Group**屬性，然後選取**忽略**。  
  
2.  重複此步驟的屬性**地區**。  
  
3.  按一下 資料表名稱旁邊的加號**v Assoc Seq Line Items**，以展開的資料表，並檢視巢狀資料表的資料行。  
  
     新模型應該只包含下列資料行：  
  
     **順序 NumberKey**  
  
     **列數字鍵**  
  
     **預測模型**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>若要處理新的時序群集模型  
  
1.  在**採礦模型**索引標籤上，以滑鼠右鍵按一下名為新的模型`Sequence Clustering`，然後選取**處理序模型**。  
  
     由於簡化的新採礦模型所根據的結構已經過處理，因此您不需要重新處理結構。 您可以只處理新的採礦模型。  
  
2.  按一下 **是**若要更新的資料採礦專案部署至伺服器。  
  
3.  在 [**處理採礦模型**] 對話方塊中，按一下**執行**。  
  
4.  按一下 [**關閉**以關閉**處理進度**對話方塊，然後再按一下**關閉**中再次**處理採礦模型**] 對話方塊。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [時序群集模型上建立預測&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [處理需求和考量 (資料採礦)](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
