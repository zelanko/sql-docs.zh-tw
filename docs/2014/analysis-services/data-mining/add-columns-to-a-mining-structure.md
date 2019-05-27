---
title: 資料行加入採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- columns [data mining], mining structure columns
- adding columns
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85a713bb9da24a67ebe8fdd097535c5a9d5ac98e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086230"
---
# <a name="add-columns-to-a-mining-structure"></a>將資料行加入至採礦結構
  使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的資料採礦設計師，即可將資料行加入至您在資料採礦精靈中定義的採礦結構。 您可以加入已存在於用來定義採礦結構之資料來源檢視中的任何資料行。  
  
> [!NOTE]  
>  您可以將資料行的多份複本加入採礦結構；不過應該避免在同一模型中使用一個以上的資料行執行個體，以避免在來源及衍生的資料行之間產生錯誤的關聯。  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>若要將資料行加入至採礦結構  
  
1.  選取資料採礦設計師中的 **[採礦結構]** 索引標籤。  
  
2.  以滑鼠右鍵按一下採礦結構，並選取 [加入資料行]。  
  
     就會開啟 **[選取資料行]** 對話方塊。  
  
3.  在 **[來源資料表]** 之下，選取資料來源檢視中該資料行所在的資料表。  
  
4.  在 **[來源資料行]** 之下，選取您要加入至採礦結構的資料行。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  如果您要加入的資料行已存在，其副本會併入結構中，並在名稱後面附加「1」。 您可藉由在採礦結構資料行的 **[名稱]** 屬性中輸入新名稱，將複製資料行的名稱變更為更具描述性的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構工作和操作說明](mining-structure-tasks-and-how-tos.md)  
  
  
