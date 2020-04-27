---
title: 建立相關的時序群集模型（中繼資料採礦教學課程） |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62855871"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>建立相關的時序群集採礦模型 (中繼資料採礦教學課程)
  探索時序群集模型之後，您了解到 Region 或 Income 等其他屬性對於模型也有很大的影響。因此，若要進一步了解時序，您需要建立相關的時序群集模型，並移除與客戶人口統計有關的屬性。  
  
 在這項工作中，您將建立一個區域時序群集模型的副本，然後從模型中移除任何與時序無直接關聯的資料行。  
  
 新的模型所包含的資料行，與所依據之採礦模型的資料行完全相同。 不過，您不必從採礦結構移除資料行，只要指定新的採礦模型忽略資料行即可。  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>若要製作時序群集模型的副本  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的資料採礦設計工具中，按一下 [**採礦模型**] 索引標籤。  
  
2.  以滑鼠右鍵按一下您要複製的模型，然後選取 [新增] [**採礦模型**]。  
  
3.  在 [**新增採礦模型**] 對話方塊中，輸入模型名稱，然後選取 [ `Sequence Clustering`Microsoft]。  
  
     在此教學課程中，請`Sequence Clustering`輸入名稱。  
  
4.  按一下 [確定]  。  
  
### <a name="to-remove-columns-from-the-mining-model"></a>若要從採礦模型移除資料行  
  
1.  在 [**採礦模型**] 索引標籤中，于名為 [時序群集] 的新模型之資料行中，按一下 [**收入群組**] 屬性的資料列，然後選取 [**忽略**]。  
  
2.  針對屬性**區域**重複此步驟。  
  
3.  按一下資料表名稱旁邊的加號 [ **v Assoc Seq Line Items**]，以展開資料表並查看嵌套資料表中的資料行。  
  
     新模型應該只包含下列資料行：  
  
     **訂單 NumberKey**  
  
     **行號索引鍵**  
  
     **模型預測**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>若要處理新的時序群集模型  
  
1.  在 [**採礦模型**] 索引標籤中，以滑鼠右鍵`Sequence Clustering`按一下名為的新模型，然後選取 [**處理模型**]。  
  
     由於簡化的新採礦模型所根據的結構已經過處理，因此您不需要重新處理結構。 您可以只處理新的採礦模型。  
  
2.  按一下 **[是]** ，將更新的資料採礦專案部署到伺服器。  
  
3.  在 [**處理採礦模型**] 對話方塊中，按一下 [**執行**]。  
  
4.  按一下 [**關閉**] 以關閉 [**處理進度**] 對話方塊，然後在 [**處理採礦模型**] 對話方塊中再次按一下 [**關閉**]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [在時序群集模型上建立預測 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [處理需求和考量 (資料採礦)](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
