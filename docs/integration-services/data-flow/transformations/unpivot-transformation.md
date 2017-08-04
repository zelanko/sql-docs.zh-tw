---
title: "取消樞紐轉換 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d491bb19b4eb86bd0fe75a7b8ca8e7b6e5d226b5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="unpivot-transformation"></a>取消樞紐轉換
  「取消樞紐」轉換可以使非正規化的資料集變成較正規化的版本，方法是將單一記錄中多個資料行的值擴充為單一資料行中具有同一值的多個記錄。 例如，列出客戶名稱的資料集對每個客戶都具有一個資料列，同時產品及購買數量會顯示在資料列的資料行中。 當「取消樞紐」轉換將資料集正規化之後，資料集便會對客戶購買的每種產品包含不同的資料列。  
  
 下圖顯示資料在 Product 資料行上取消樞紐之前的資料集。  
  
 ![取消樞紐之後的資料集](../../../integration-services/data-flow/transformations/media/mw-dts-18.gif "取消樞紐之後的資料集")  
  
 下圖顯示在 Product 資料行上取消樞紐之後的資料集。  
  
 ![取消樞紐之前的資料集](../../../integration-services/data-flow/transformations/media/mw-dts-17.gif "取消樞紐之前的資料集")  
  
 在某些情況下，取消樞紐結果可能會包含非預期之值的資料列。 例如，如果圖表中顯示為要取消樞紐的範例資料中，Fred 的所有 Qty 資料行中都有 Null 值，那麼在輸出中只會包含一個 Fred 的資料列，而不是五個。 視資料行資料類型而定，Qty 資料行可能包含 Null 或零。  
  
## <a name="configuration-of-the-unpivot-transformation"></a>設定取消樞紐轉換  
 取消樞紐轉換包括 **PivotKeyValue** 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 此轉換有一個輸入和一個輸出。 但沒有錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [取消樞紐轉換編輯器] 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [取消樞紐轉換編輯器](../../../integration-services/data-flow/transformations/unpivot-transformation-editor.md)  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
  
