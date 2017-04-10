---
title: "處理採礦模型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "採礦模型 [Analysis Services], 處理"
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 32
---
# 處理採礦模型
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料採礦設計師的 [採礦模型] 索引標籤中，您可以處理與採礦結構相關聯的特定採礦模型，或處理與結構相關聯的所有模型。  
  
 您可以使用下列工具處理採礦模型：  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 您也可以使用 XMLA 處理命令。 如需詳細資訊，請參閱[處理的工具和方式 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)。  
  
### 使用 SQL Server 資料工具處理單一採礦模型  
  
1.  在 [資料採礦設計師] 的 [採礦模型] 索引標籤上，從方格中模型的一或多個資料行選取採礦模型。  
  
2.  在 [採礦模型] 功能表上，選取 [處理模型]。  
  
     如果您變更了採礦結構，在處理模型之前，會提示您重新部署結構。 按一下 **[是]**。  
  
3.  在 [Processing Mining Model - \<model> (處理採礦模型 - \<模型>)] 對話方塊中，按一下 [執行]。  
  
     [處理進度] 對話方塊就會開啟，以顯示模型處理的詳細資料。  
  
4.  在模型順利完成處理之後，按一下 [處理進度] 對話方塊中的 [關閉]。  
  
5.  在 [Processing Mining Model - \<model> (處理採礦模型 - \<模型>)] 對話方塊中，按一下 [關閉]。  
  
 只處理採礦結構和選取的採礦模型。  
  
### 處理與採礦結構相關聯的所有採礦模型  
  
1.  在 [資料採礦設計師] 的 [採礦模型] 索引標籤上，從 [採礦模型] 功能表中選取 [處理採礦結構和所有模型]。  
  
2.  如果您變更了採礦結構，在處理模型之前，會提示您重新部署結構。 按一下 **[是]**。  
  
3.  在 [Processing Mining Structure - \<structure> (處理採礦結構 - \<結構>)] 對話方塊中，按一下 [執行]。  
  
4.  [處理進度] 對話方塊就會開啟，以顯示模型處理的詳細資料。  
  
5.  在模型順利完成處理之後，按一下 [處理進度] 對話方塊中的 [關閉]。  
  
6.  在 [Processing \<model> (處理 \<模型>)] 對話方塊中，按一下 [關閉]。  
  
 已處理採礦結構和所有相關聯的採礦模型。  
  
## 請參閱＜  
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  