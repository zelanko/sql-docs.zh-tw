---
title: "將資料行加入至採礦結構 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "採礦結構 [Analysis Services], 資料行"
  - "資料行 [資料採礦], 採礦結構資料行"
  - "加入資料行"
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 30
---
# 將資料行加入至採礦結構
  使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的資料採礦設計師，即可將資料行加入至您在資料採礦精靈中定義的採礦結構。 您可以加入已存在於用來定義採礦結構之資料來源檢視中的任何資料行。  
  
> [!NOTE]  
>  您可以將資料行的多份複本加入採礦結構；不過應該避免在同一模型中使用一個以上的資料行執行個體，以避免在來源及衍生的資料行之間產生錯誤的關聯。  
  
### 若要將資料行加入至採礦結構  
  
1.  選取資料採礦設計師中的 **[採礦結構]** 索引標籤。  
  
2.  以滑鼠右鍵按一下採礦結構，並選取 [加入資料行]。  
  
     就會開啟 **[選取資料行]** 對話方塊。  
  
3.  在 **[來源資料表]**之下，選取資料來源檢視中該資料行所在的資料表。  
  
4.  在 **[來源資料行]**之下，選取您要加入至採礦結構的資料行。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  如果您要加入的資料行已存在，其副本會併入結構中，並在名稱後面附加「1」。 您可藉由在採礦結構資料行的 **[名稱]** 屬性中輸入新名稱，將複製資料行的名稱變更為更具描述性的名稱。  
  
## 請參閱＜  
 [採礦結構工作和使用說明](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  