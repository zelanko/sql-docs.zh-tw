---
title: "資料轉換 」 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataconversiontrans.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 897651a9257aadeac68a392eeae8b51d0c87de8d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="data-conversion-transformation"></a>資料轉換
  「資料轉換」會將輸入資料行中的資料轉換成不同的資料類型，然後將它複製到新的輸出資料行。 例如，封裝可從多個來源擷取資料，然後使用此轉換將資料行轉換成目的地資料存放區所需的資料類型。 您可以對單一輸入資料行套用多項轉換。  
  
 使用此轉換，封裝即可執行下列類型的資料轉換：  
  
-   變更資料類型。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
    > [!NOTE]  
    >  如果您要將資料轉換成日期或日期時間資料類型，則輸出資料行中的資料會使用 ISO 格式，即使地區設定偏好設定可能指定不同的格式。  
  
-   設定字串資料的資料行長度，以及數值資料的有效位數和小數位數。 如需詳細資訊，請參閱[有效位數、小數位數和長度 &#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
-   指定字碼頁。 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。  
  
    > [!NOTE]  
    >  在字串資料類型的資料行之間進行複製時，兩個資料行必須使用相同字碼頁。  
  
 如果字串資料的輸出資料行長度比其對應輸入資料行的長度短，則輸出資料會遭到截斷。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../../integration-services/data-flow/error-handling-in-data.md)。  
  
 這個轉換有一個輸入、一個輸出與一個錯誤輸出。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。 如需在 SSIS 設計師中使用「資料轉換」的相關資訊，請參閱 [使用資料轉換將資料轉換至不同的資料類型](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md) 和 [資料轉換編輯器](../../../integration-services/data-flow/transformations/data-conversion-transformation-editor.md)。 如需以程式設計方式設定此轉換屬性的詳細資訊，請參閱 [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) 和 [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
## <a name="related-content"></a>相關內容  
 blogs.msdn.com 上的部落格文章： [SSIS 2008 中各種資料類型轉換技術的效能比較](http://go.microsoft.com/fwlink/?LinkId=220823)。  
  
## <a name="see-also"></a>請參閱＜  
 [快速剖析](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
