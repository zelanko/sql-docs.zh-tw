---
title: 合併聯結轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6f6f584d49bfa238a5eda76b18f0dccb59db303f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186828"
---
# <a name="merge-join-transformation-editor"></a>合併聯結轉換編輯器
  使用 [合併聯結轉換編輯器] 對話方塊，即可指定合併兩個由聯結組合之輸入的聯結類型、聯結資料行以及輸出資料行。  
  
> [!IMPORTANT]  
>  合併聯結轉換針對其輸入需要已排序的資料。 如需這項重要需求的詳細資訊，請參閱 [排序合併和合併聯結轉換的資料](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
 若要深入了解合併聯結轉換，請參閱 [合併聯結轉換](data-flow/transformations/merge-join-transformation.md)。  
  
## <a name="options"></a>選項。  
 **聯結類型**  
 指定要使用內部聯結、左方外部聯結或完整聯結。  
  
 **交換輸入**  
 使用 [交換輸入] 按鈕，來切換輸入之間的順序。 此選取項目對於左方外部聯結選項可能非常有用。  
  
 **輸入**  
 針對您要放入合併輸出中的每個資料行，首先從可用的輸入清單中選取。  
  
 輸入會以兩個個別的資料表來顯示。 選取要包含在輸出中的資料行。 拖曳資料行以建立資料表之間的聯結。 若要刪除聯結，請選取聯結然後按下 DELETE 鍵。  
  
 **輸入資料行**  
 從所選輸入上之可用的資料行清單中，選取要包含在合併輸出中的資料行。  
  
 **輸出別名**  
 輸入每一個輸出資料行的別名。 預設是輸入資料行的名稱；但是，您可以選擇任何唯一的、描述性名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [排序合併和合併聯結轉換的資料](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [使用合併聯結轉換來擴充資料集](data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [合併轉換](data-flow/transformations/merge-transformation.md)   
 [聯集全部轉換](data-flow/transformations/union-all-transformation.md)  
  
  
