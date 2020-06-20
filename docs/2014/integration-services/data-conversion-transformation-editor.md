---
title: 資料轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b452acb2e9d168910fec06d959ce3a1c1704b814
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917078"
---
# <a name="data-conversion-transformation-editor"></a>資料轉換編輯器
  使用 [資料轉換編輯器]**** 對話方塊，即可選取要轉換的資料行、選取資料行要轉換成哪一種資料類型，以及設定轉換屬性。  
  
> [!NOTE]  
>  [資料轉換 `FastParse` **編輯器**] 中無法使用資料轉換之輸出資料行的屬性，但是可以使用 [**進階編輯器**] 來設定它。 如需這個屬性的詳細資訊，請參閱 [轉換自訂屬性](data-flow/transformations/transformation-custom-properties.md)的＜資料轉換＞一節。  
  
 若要深入了解資料轉換，請參閱 [資料轉換](data-flow/transformations/data-conversion-transformation.md)。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用核取方塊選取要轉換的資料行。 您的選取範圍會將輸入資料行加入下列資料表中。  
  
 **輸入資料行**  
 從可用的輸入資料行清單中，選取要轉換的資料行。 您的選擇會反映在上面所勾選的核取方塊中。  
  
 **輸出別名**  
 輸入每一個新資料行的別名。 預設為 `Copy of`，後面接著輸入資料行的名稱；但是您也可以選擇任何唯一的描述性名稱。  
  
 **資料類型**  
 從清單中選取可用的資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
 **長度**  
 設定字串資料的資料行長度。  
  
 **有效位數**  
 設定數值資料的有效位數。  
  
 **縮放比例**  
 設定數值資料的小數位數。  
  
 **字碼頁**  
 為 DT_STR 類型的資料行選取適當的字碼頁。  
  
 **設定錯誤輸出**  
 使用 [設定錯誤輸出](../../2014/integration-services/configure-error-output.md) 對話方塊來指定如何處理資料列層級錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用資料轉換將資料轉換至不同的資料類型](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  
