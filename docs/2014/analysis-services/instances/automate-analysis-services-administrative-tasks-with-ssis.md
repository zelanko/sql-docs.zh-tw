---
title: 使用 SSIS Analysis Services 管理工作自動化 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Execute DDL Task [Analysis Services]
- Analysis Services Processing task
ms.assetid: e960a9a2-80b4-45da-9369-bc560ecdccac
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a06a04c50dbb1548ac28902dcfb2f7f7a2883232
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023681"
---
# <a name="automate-analysis-services-administrative-tasks-with-ssis"></a>使用 SSIS 自動化 Analysis Services 管理工作
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可讓您自動執行 DDL 指令碼、Cube 和採礦模型處理工作，以及資料採礦查詢工作。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可視為控制流程和維護工作的集合，可以連結它們來形成循序和平行的資料處理作業。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可以在執行資料處理工作期間進行資料清除作業，以及匯集來自不同資料來源的資料。 使用 Cube 和採礦模型時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可以將非數值資料轉換為數值資料，且可以確定資料值會落在預期的界限內，從而建立用來擴展事實資料表和維度的全新資料。  
  
## <a name="integration-services-tasks"></a>Integration Services 工作  
 任何 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作或作業中有兩個主要元素：控制流程元素和資料流程元素。 控制流程元素會套用優先順序條件約束來定義作業進行的邏輯順序。 資料流程元素涉及到元件輸出和接續元件輸入之間的連接性，加上在中間資料上執行的任何資料轉換。 至於資料流向的決策，優先順序條件約束會包含邏輯來指定由哪個元件接收輸出。 與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工作包含執行 DDL 工作、Analysis Services 處理工作，以及資料採礦查詢工作。 針對其中每一項工作，可以使用傳送郵件工作將包含工作結果的電子郵件訊息傳送給管理員。  
  
## <a name="the-execute-ddl-task"></a>執行 DDL 工作  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的執行 DDL 工作，可讓您直接傳送 DDL 指令碼至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器並自動執行。 這樣可讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理員從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝內執行備份、還原或同步處理作業。 封裝是由稍早所述的控制和資料流程元素組成，全部元素必須 **run regularly**，就像其他可加入工作中的 DDL 陳述式一樣。 因為此處所討論的工作經常在夜晚執行，可以輕易地從任何排程應用程式執行的封裝就非常有用。 您可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Agent 來排程封裝在任何時間執行。 如需如何實作這項工作的詳細資訊，請參閱 [Analysis Services 執行 DDL 工作](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)。  
  
## <a name="analysis-services-processing-task"></a>Analysis Services 處理工作  
 當您定期更新來源關聯式資料庫時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的 Analysis Services 處理工作可讓您自動以新資訊擴展 Cube。 您可以使用 Analysis Services 處理工作在維度、Cube 或資料分割層級上處理。 處理本身可以是 `incremental`或 `full`類型，您需要根據作業需求來選取類型。 累加式處理會加入新資料並執行足夠的重新計算，讓目標保持最新，反之，完整處理會卸除現有的資料，以執行完全重新載入和重新計算。 完整處理花費的時間較久，但較為完整。 如需有關如何實作這項工作的詳細資訊，請參閱＜ [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md)＞。  
  
## <a name="data-mining-query-task"></a>資料採礦查詢工作  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的資料採礦查詢工作，可讓您在採礦模型中擷取和儲存資訊。 資訊通常會儲存在關聯式資料庫，且 (例如) 可用來隔離目標行銷活動的潛在客戶清單。 資料採礦可以識別客戶的值和客戶回應特定行銷廣告的機率。 您可以使用資料採礦查詢工作來擷取和修改資料為慣用的格式。 如需有關如何實作這項工作的詳細資訊，請參閱＜ [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割處理目的地](../../integration-services/data-flow/partition-processing-destination.md)   
 [維度處理目的地](../../integration-services/data-flow/dimension-processing-destination.md)   
 [資料採礦查詢轉換](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)   
 [多維度模型物件處理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services 中的指令碼管理工作](../script-administrative-tasks-in-analysis-services.md)  
  
  