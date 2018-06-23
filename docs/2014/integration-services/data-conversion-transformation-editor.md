---
title: 資料轉換編輯器 |Microsoft 文件
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
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9c5157175181c7a43a2c8e3209c23905a4129d2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031685"
---
# <a name="data-conversion-transformation-editor"></a>資料轉換編輯器
  使用 [資料轉換編輯器] 對話方塊，即可選取要轉換的資料行、選取資料行要轉換成哪一種資料類型，以及設定轉換屬性。  
  
> [!NOTE]  
>  `FastParse`的 「 資料轉換 」 轉換之輸出資料行的屬性不適用於**資料轉換編輯器**，但是可以透過設定**進階編輯器**。 如需這個屬性的詳細資訊，請參閱[轉換自訂屬性](data-flow/transformations/transformation-custom-properties.md)的＜資料轉換＞一節。  
  
 若要深入了解資料轉換，請參閱 [資料轉換](data-flow/transformations/data-conversion-transformation.md)。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用核取方塊選取要轉換的資料行。 您的選取範圍會將輸入資料行加入下列資料表中。  
  
 **輸入資料行**  
 從可用的輸入資料行清單中，選取要轉換的資料行。 您的選擇會反映在上面所勾選的核取方塊中。  
  
 **輸出別名**  
 輸入每一個新資料行的別名。 預設值是`Copy of`後面輸入資料行名稱; 不過，您可以選擇任何唯一的、 描述性的名稱。  
  
 **資料類型**  
 從清單中選取可用的資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
 **長度**  
 設定字串資料的資料行長度。  
  
 **有效位數**  
 設定數值資料的有效位數。  
  
 **小數位數**  
 設定數值資料的小數位數。  
  
 **字碼頁**  
 為 DT_STR 類型的資料行選取適當的字碼頁。  
  
 **設定錯誤輸出**  
 使用 [設定錯誤輸出](../../2014/integration-services/configure-error-output.md) 對話方塊來指定如何處理資料列層級錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用資料轉換將資料轉換至不同的資料類型](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  