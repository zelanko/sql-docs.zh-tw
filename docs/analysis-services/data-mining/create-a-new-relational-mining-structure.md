---
title: "建立新的關聯式採礦結構 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], relational
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
ms.assetid: 55bac3bd-700e-4f91-bcc6-f3cd8c026da1
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6784d7ab5e13d5e842794041589db515a6fd2a30
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-new-relational-mining-structure"></a>建立新的關聯式採礦結構
  使用 [資料採礦精靈] 建立新的採礦結構 (利用關聯式資料庫或其他來源中的資料)，然後將此結構和任何相關模型儲存到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
## <a name="to-create-a-relational-mining-structure"></a>若要建立關聯式採礦結構  
  
1.  在方案總管中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中的 [採礦結構] 資料夾，然後按一下 [新增採礦結構]。  
  
     就會開啟資料採礦精靈。  
  
2.  在 **[歡迎使用資料採礦精靈]** 頁面上，按 **[下一步]**。  
  
3.  在 [選取定義方法] 頁面上，選取 [從現有的關聯式資料庫或資料倉儲]，然後按一下 [下一步]。  
  
4.  在 [選取資料採礦技術] 頁面上，選取您要使用的資料採礦演算法，然後按一下 [下一步]。  
  
     如需資料採礦演算法的詳細資訊，請參閱[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
5.  在 [選取資料來源檢視] 頁面上，在 [可用的資料來源檢視] 之下，按一下您要使用的資料來源檢視，然後按一下 [下一步]。  
  
     如需建立資料來源檢視的詳細資訊，請參閱[多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
6.  在 [指定資料表類型] 頁面上，[輸入資料表] 之下，選取案例資料表和巢狀資料表。  
  
7.  在 [指定培訓資料] 頁面上，[採礦模型結構] 之下，選取索引鍵、輸入和可預測資料行。  
  
     在選取可預測資料行之後，您可以按一下 [建議] 按鈕來開啟 [建議相關資料行] 對話方塊。 您可以按一下此對話方塊中的 [確定] 來接受建議的資料行，在採礦結構中包含選取的資料行，或先在 [輸入] 資料行中變更選擇，然後按一下 [確定]。 若要忽略建議，請按一下 [取消]。  
  
8.  按一下 **[下一步]**。  
  
9. 在 [指定資料行的內容和資料類型] 頁面上，在 [採礦模型結構] 之下，您可以調整每一個資料行的內容類型和資料類型。  
  
    > [!NOTE]  
    >  您可以按一下 [偵測]，來自動偵測資料行是包含連續或分隔資料。 按一下此按鈕之後，資料行內容和資料類型將在 [內容類型] 和 [資料類型] 資料行中更新。 如需內容類型及資料類型的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md) 和[資料類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/data-types-data-mining.md)。  
  
10. 按一下 **[下一步]**。  
  
11. 在 [正在完成精靈] 頁面上，提供採礦結構的名稱和要建立的相關初始採礦模型，然後按一下 [完成]。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和使用說明](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  

