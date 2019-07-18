---
title: 資料轉換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontrans.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 762bf6b25fec66f5281d32ca9c5d15aa6e64ce31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770434"
---
# <a name="data-conversion-transformation"></a>資料轉換
  「資料轉換」會將輸入資料行中的資料轉換成不同的資料類型，然後將它複製到新的輸出資料行。 例如，封裝可從多個來源擷取資料，然後使用此轉換將資料行轉換成目的地資料存放區所需的資料類型。 您可以對單一輸入資料行套用多項轉換。  
  
 使用此轉換，封裝即可執行下列類型的資料轉換：  
  
-   變更資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../integration-services-data-types.md)。  
  
    > [!NOTE]  
    >  如果您要將資料轉換成日期或日期時間資料類型，則輸出資料行中的資料會使用 ISO 格式，即使地區設定偏好設定可能指定不同的格式。  
  
-   設定字串資料的資料行長度，以及數值資料的有效位數和小數位數。 如需詳細資訊，請參閱[有效位數、小數位數和長度 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/precision-scale-and-length-transact-sql)。  
  
-   指定字碼頁。 如需詳細資訊，請參閱 [Comparing String Data](../comparing-string-data.md)。  
  
    > [!NOTE]  
    >  在字串資料類型的資料行之間進行複製時，兩個資料行必須使用相同字碼頁。  
  
 如果字串資料的輸出資料行長度比其對應輸入資料行的長度短，則輸出資料會遭到截斷。 如需詳細資訊，請參閱 [處理資料中的錯誤](../error-handling-in-data.md)。  
  
 這個轉換有一個輸入、一個輸出與一個錯誤輸出。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。 如需在 SSIS 設計師中使用「資料轉換」的相關資訊，請參閱 [使用資料轉換將資料轉換至不同的資料類型](data-conversion-transformation.md) 和 [資料轉換編輯器](../../data-conversion-transformation-editor.md)。 如需以程式設計方式設定此轉換屬性的詳細資訊，請參閱 [通用屬性](../../common-properties.md) 和 [轉換自訂屬性](transformation-custom-properties.md)。  
  
## <a name="related-content"></a>相關內容  
 blogs.msdn.com 上的部落格文章： [SSIS 2008 中各種資料類型轉換技術的效能比較](https://go.microsoft.com/fwlink/?LinkId=220823)。  
  
## <a name="see-also"></a>另請參閱  
 [快速剖析](../../fast-parse.md)   
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
