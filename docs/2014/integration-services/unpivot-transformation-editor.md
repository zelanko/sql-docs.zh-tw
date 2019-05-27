---
title: 取消樞紐轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottransformation.f1
helpviewer_keywords:
- Unpivot Transformation Editor
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a0222627860b70059163bff1dd989e230c1cb66
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054843"
---
# <a name="unpivot-transformation-editor"></a>取消樞紐轉換編輯器
  使用 **[取消樞紐轉換編輯器]** 對話方塊，即可選取要樞紐轉換為資料列的資料行，以及指定資料行和新的樞紐值輸出資料行。  
  
> [!NOTE]  
>  此主題依賴於 [取消樞紐轉換](data-flow/transformations/unpivot-transformation.md) 中所描述的取消樞紐狀況，來說明選項的使用。  
  
 若要深入了解取消樞紐轉換，請參閱＜ [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用此核取方塊，指定要樞紐轉換為資料列的資料行。  
  
 **名稱**  
 檢視可用輸入資料行的名稱。  
  
 **通過**  
 指出是否將資料行包含在取消樞紐的輸出中。  
  
 **輸入資料行**  
 從每個資料列的可用輸入資料行清單中選取。 您的選擇會反映在 **[可用的輸入資料行]** 資料表的核取方塊選擇中。  
  
 在＜ [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)＞所描述的取消樞紐狀況中，輸入資料行是 **Ham**, **Soda**, **Milk**, **Beer**和 **Chips** 資料行。  
  
 **目的地資料行**  
 提供資料行的名稱。  
  
 在 [取消樞紐轉換](data-flow/transformations/unpivot-transformation.md)所描述的取消樞紐狀況中，目的地資料行就是數量 (**Qty**) 資料行。  
  
 **樞紐索引鍵值**  
 提供樞紐值的名稱。 預設是輸入資料行的名稱；但是，您可以選擇任何唯一的、描述性名稱。  
  
 此屬性的值可以使用屬性運算式指定。  
  
 在＜ [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)＞所描述的取消樞紐狀況中，樞紐值會在 **[樞紐索引鍵值資料行名稱]** 選項所指定之新 Product 資料行中顯示為下列文字值： **Ham**, **Soda**, **Milk**, **Beer**和 **Chips**。  
  
 **[樞紐索引鍵值資料行名稱]**  
 提供樞紐值資料行的名稱。 預設為「樞紐索引鍵值」；然而，您可以選擇任何唯一的、描述性名稱。  
  
 在＜ [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)＞所描述的取消樞紐狀況中，樞紐索引鍵值資料行名稱為 **Product** ，並且會將新的 **Product** 資料行指定給 **Ham**, **Soda**, **Milk**, **Beer**和 **Chips** 資料行，以取消樞紐。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [樞紐轉換](data-flow/transformations/pivot-transformation.md)  
  
  
