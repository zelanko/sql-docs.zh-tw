---
title: CDC 來源編輯器 （資料行頁面） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.cdcsource.columns.f1
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 87d5d9b1096e2068759a2100b4daf504849fba0e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035030"
---
# <a name="cdc-source-editor-columns-page"></a>CDC 來源編輯器 (資料行頁面)
  使用 [CDC 來源編輯器] 對話方塊的 [資料行] 頁面，即可將輸出資料行對應至每個外部 (來源) 資料行。  
  
 若要了解有關 CDC 來源的詳細資訊，請參閱＜ [CDC Source](data-flow/cdc-source.md)＞。  
  
## <a name="task-list"></a>工作清單  
 **若要開啟 CDC 來源編輯器的資料行頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，開啟具有 CDC 來源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 CDC 來源。  
  
3.  在 **[CDC 來源編輯器]** 中，按一下 **[資料行]**。  
  
## <a name="options"></a>選項。  
 **可用的外部資料行**  
 資料來源中可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。 請在來源中選取要使用的資料行。 選取的資料行就會依照選取的順序加入至 **[外部資料行]** 清單。  
  
 **[外部資料行]**  
 外部 (來源) 資料行的檢視，這些資料行會依照您在設定取用 CDC 來源資料之元件時所看見的順序列出。 若要變更此順序，請先清除 **[可用的外部資料行]** 清單中的選取資料行，然後依照不同的順序，從清單選取外部資料行。 選取的資料行就會依照您選取的順序加入至 **[外部資料行]** 清單。  
  
 **輸出資料行**  
 為每個輸出資料行輸入唯一的名稱。 預設值為選取之外部 (來源) 資料行的名稱。不過，您也可以選擇任何唯一的描述性名稱。 輸入的名稱就會顯示在 SSIS 設計師中。  
  
## <a name="see-also"></a>另請參閱  
 [CDC 來源編輯器&#40;連接管理員頁面&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [CDC 來源編輯器&#40;錯誤輸出頁面&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  