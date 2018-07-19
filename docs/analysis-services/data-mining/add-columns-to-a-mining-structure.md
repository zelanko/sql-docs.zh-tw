---
title: 資料行加入採礦結構 |Microsoft 文件
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c09d4b263dc4e4274888f6cbd8bf1f27103dd8b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34016286"
---
# <a name="add-columns-to-a-mining-structure"></a>將資料行加入至採礦結構
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [採礦結構工作和使用說明](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
