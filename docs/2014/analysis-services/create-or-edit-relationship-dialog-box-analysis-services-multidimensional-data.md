---
title: 建立或編輯關聯性對話方塊 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dsvdesigner.createrelationship.f1
helpviewer_keywords:
- Create Relationship dialog box
ms.assetid: da3c7074-623e-4ddf-a707-d3276a47cf1c
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c205a2f7c78345d77dd3080b9ef33fe87f87ba35
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133336"
---
# <a name="create-or-edit-relationship-dialog-box-analysis-services---multidimensional-data"></a>建立或編輯關聯性對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [Create/Edit Relationship (建立/編輯關聯性)] 對話方塊，即可定義或修改資料來源檢視中的關聯性。 您可以用下列方式來顯示 [Create/Edit Relationship (建立/編輯關聯性)] 對話方塊：  
  
-   按一下 [Data Source View Designer (資料來源檢視設計工具)] 之 [工具列] 窗格中的 [新增關聯性]。  
  
-   以滑鼠右鍵按一下 [Data Source View Designer (資料來源檢視設計工具)] 之 [資料表] 或 [圖表] 窗格中的資料表，並選取 [新增關聯性]。  
  
-   以滑鼠右鍵按一下 [Data Source View Designer (資料來源檢視設計工具)] 之 [圖表] 窗格中的關聯性，並選取 [編輯關聯性]。  
  
> [!NOTE]  
>  您可以在 [資料來源檢視設計師] 中，建立不存在於基礎資料來源的關聯性，也可以從基礎資料來源的現有外部索引鍵關聯性，移除**資料來源檢視設計師**所建立的關聯性。  
  
## <a name="options"></a>選項。  
 **來源 （外部索引鍵） 資料表**  
 選取包含參考目的地資料表中之一個或多個資料行的資料表或具名查詢。  
  
 **目的地 （主索引鍵） 資料表**  
 選取包含來源資料表所參考之一個或多個資料行的資料表。 針對自我聯結，選取與在 [來源 (外部索引鍵) 資料表] 中所選取的相同資料表。  
  
 **來源資料行**  
 選取會參考目的地資料表中之資料行的資料行。  
  
 **目的地資料行**  
 選取來源資料表中之資料行所參考的資料行。  
  
 **反轉**  
 按一下即可反轉關聯性的方向。  
  
 **說明**  
 選擇性地鍵入關聯性的描述。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [資料來源檢視設計師&#40;Analysis Services-多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  