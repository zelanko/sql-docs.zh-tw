---
title: 聯集全部轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- Union All Transformation Editor
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b62fb5e33311f1011911c40fc858723b218bac55
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054825"
---
# <a name="union-all-transformation-editor"></a>聯集全部轉換編輯器
  使用 **[聯集全部轉換編輯器]** 對話方塊，即可將數個輸入資料列集合併至單一輸出資料列集。 藉由在資料流程中包含聯集全部轉換，您可以合併多個資料流程中的資料、藉由巢狀聯集全部轉換來建立複雜資料集、以及更正資料中的錯誤之後重新合併資料列。  
  
 若要深入了解聯集全部轉換，請參閱＜ [Union All Transformation](data-flow/transformations/union-all-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **輸出資料行名稱**  
 輸入每個資料行的別名。 預設值為第一個 (參考) 輸入的輸入資料行名稱；不過，您也可以選擇任何唯一的、描述性的名稱。  
  
 **聯集全部輸入 1**  
 從第一個 (參考) 輸入的可用輸入資料行清單中選取。 對應資料行的中繼資料必須相符。  
  
 **聯集全部輸入 n**  
 從第二個和其他輸入的可用輸入資料行清單中選取。 對應資料行的中繼資料必須相符。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用聯集全部轉換來合併資料](data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [合併轉換](data-flow/transformations/merge-transformation.md)   
 [合併聯結轉換](data-flow/transformations/merge-join-transformation.md)  
  
  
