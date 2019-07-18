---
title: 建立預測結構和模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e631a8983705d4f58e4b193823c9a255284f346
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204807"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>建立預測結構和模型 (中繼資料採礦教學課程)
  接下來，您將使用資料採礦精靈，根據您剛建立的資料來源檢視建立新的採礦結構和採礦模型。 在這項工作中，您將指定採礦模型應使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法。  
  
### <a name="to-create-a-forecasting-mining-structure"></a>若要建立預測採礦結構  
  
1.  在 [方案總管] 中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，以滑鼠右鍵按一下**採礦結構**，然後選取**New Mining Structure&lt**。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]** 。  
  
3.  在 [**選取定義方法**頁面上，確認**從現有的關聯式資料庫或資料倉儲**已選取，然後按一下**下一步]** 。  
  
4.  在上**建立資料採礦結構**頁面的 **您想要使用哪一種資料採礦技術？** ，選取**Microsoft 時間序列**，然後按一下  **下一步**。  
  
5.  在 **選取資料來源檢視**頁面的 **可用的資料來源檢視**，選取**SalesByRegion**。  
  
6.  按一下 [下一步]  。  
  
7.  在上**指定資料表類型**頁面上，確認中的核取方塊**案例**vTimeSeries 資料表的資料行已選取，然後再按**下一步**。  
  
8.  在 **指定培訓資料**頁面上，選取核取方塊後**金鑰**ModelRegion 和 ReportingDate 資料行的資料行。  
  
     ReportingDate 應該已依預設選取，因為您在建立資料來源檢視時，已將這個資料行指定為邏輯主索引鍵。 加入 ModelRegion 做為第二個索引鍵時，等於要求演算法針對列於此欄位上的各模型與區域組合，建立個別的時間序列。  
  
9. 選取核取方塊後**輸入**並**Predictable**為數量、 資料行，然後按一下資料行**下一步**。  
  
     藉由選取**Predictable**，代表您要對此資料行中的資料建立預測。 不過，由於您要根據過去的資料進行預測，因此您必須加入資料行做為輸入內容。  
  
10. 該頁**指定資料行的內容和資料類型**，檢閱所做的選擇。  
  
     ModelRegion 資料行指定為**金鑰**資料行和 ReportingDate 資料行被自動指定為**Key Time**資料行。 每一種類型的索引鍵，您只能有一個。  
  
11. 按一下 [下一步]  。  
  
12. 在上**完成精靈**頁面上，如**採礦結構名稱**，型別`Forecasting`。  
  
    > [!NOTE]  
    >  在時間序列模型中，不提供啟用鑽研的選項。  
  
13. 在 **採礦模型名稱**，型別`Forecasting`，然後按一下**完成**。  
  
     資料採礦設計師會開啟並顯示`Forecasting`您剛才建立的採礦結構。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [修改預測結構&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦設計師](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
