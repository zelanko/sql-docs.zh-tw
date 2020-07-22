---
title: 資料轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataconversiontrans.f1
- sql13.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e43b29fadf9c4fe36775616a8ddf7a82a29eae4e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912303"
---
# <a name="data-conversion-transformation"></a>資料轉換

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  「資料轉換」會將輸入資料行中的資料轉換成不同的資料類型，然後將它複製到新的輸出資料行。 例如，封裝可從多個來源擷取資料，然後使用此轉換將資料行轉換成目的地資料存放區所需的資料類型。 您可以對單一輸入資料行套用多項轉換。  
  
 使用此轉換，封裝即可執行下列類型的資料轉換：  
  
-   變更資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
    > [!NOTE]  
    >  如果您要將資料轉換成日期或日期時間資料類型，則輸出資料行中的資料會使用 ISO 格式，即使地區設定偏好設定可能指定不同的格式。  
  
-   設定字串資料的資料行長度，以及數值資料的有效位數和小數位數。 如需詳細資訊，請參閱[有效位數、小數位數和長度 &#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
-   指定字碼頁。 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。  
  
    > [!NOTE]  
    >  在字串資料類型的資料行之間進行複製時，兩個資料行必須使用相同字碼頁。  
  
 如果字串資料的輸出資料行長度比其對應輸入資料行的長度短，則輸出資料會遭到截斷。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../../integration-services/data-flow/error-handling-in-data.md)。  
  
 這個轉換有一個輸入、一個輸出與一個錯誤輸出。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。 如需在 SSIS 設計工具中使用資料轉換的資訊，請參閱[使用資料轉換將資料轉換成不同的資料類型](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)。 如需以程式設計方式設定此轉換屬性的詳細資訊，請參閱 [通用屬性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) 和 [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
## <a name="related-content"></a>相關內容  
 blogs.msdn.com 上的部落格文章： [SSIS 2008 中各種資料類型轉換技術的效能比較](https://techcommunity.microsoft.com/t5/datacat/performance-comparison-between-data-type-conversion-techniques/ba-p/305035)。  
  
## <a name="data-conversion-transformation-editor"></a>資料轉換編輯器
  使用 [資料轉換編輯器]  對話方塊，即可選取要轉換的資料行、選取資料行要轉換成哪一種資料類型，以及設定轉換屬性。  
  
> [!NOTE]  
>  在 [資料轉換編輯器]  中無法使用資料轉換之輸出資料行的 **FastParse** 屬性，但可使用 [進階編輯器]  來設定這兩個屬性。 如需這個屬性的詳細資訊，請參閱 [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)的＜資料轉換＞一節。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用核取方塊選取要轉換的資料行。 您的選取範圍會將輸入資料行加入下列資料表中。  
  
 **輸入資料行**  
 從可用的輸入資料行清單中，選取要轉換的資料行。 您的選擇會反映在上面所勾選的核取方塊中。  
  
 **輸出別名**  
 輸入每一個新資料行的別名。 預設為輸入資料行的名稱，後面接著 **[的副本]** ；但是您也可以選擇任何唯一的描述性名稱。  
  
 **資料類型**  
 從清單中選取可用的資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
 **長度**  
 設定字串資料的資料行長度。  
  
 **有效位數**  
 設定數值資料的有效位數。  
  
 **調整**  
 設定數值資料的小數位數。  
  
 **字碼頁**  
 為 DT_STR 類型的資料行選取適當的字碼頁。  
  
 **設定錯誤輸出**  
 使用 [設定錯誤輸出](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 對話方塊來指定如何處理資料列層級錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [快速剖析](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
