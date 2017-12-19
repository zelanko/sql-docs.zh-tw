---
title: "語法 (SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- expressions [Integration Services], syntax
- syntax [Integration Services]
ms.assetid: 61c053c5-1182-4ad0-b804-51cbd19aa0ba
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 89de000e168f3b781c24662cd24928f095aed33a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="syntax-ssis"></a>語法 (SSIS)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式語法與 C 和 C# 語言使用的語法類似。 運算式的元素包括識別碼 (資料行和變數)、常值、運算子以及函數。 本主題摘要說明運算式評估工具語法套用至不同運算式元素時的獨特需求。  
  
> [!NOTE]  
>  在舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，當運算式的評估結果具有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型 DT_WSTR 或 DT_STR 時，結果就會具有 4000 個字元的限制。 這項限制已移除。  
  
 如需使用特定運算子及函數的範例運算式，請參閱下列主題中每個運算子及函數的相關主題：[運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md) 和[函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)。  
  
 如需使用多個運算子、函數以及識別碼和常值的範例運算式，請參閱[進階 Integration Services 運算式範例](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)。  
  
 如需屬性運算式中使用的範例運算式，請參閱 [在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
## <a name="identifiers"></a>識別碼  
 運算式可以包括資料行和變數識別碼。 資料行可在資料來源中產生，或在資料流程中藉由轉換建立。 運算式可以使用歷程識別碼來參考資料行。 歷程識別碼是用來識別封裝元素的唯一號碼。 運算式中參考的歷程識別碼必須包括井字號 (#) 前置詞。 例如，歷程識別碼 138 是使用 #138 參考。  
  
 運算式可包括 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 提供的系統變數和自訂變數。 在運算式中參考變數時，必須包括 @ 前置詞。 例如，`Counter` 變數是使用 @Counter 參考的。 @ 字元並非變數名稱的一部分；該字元僅用來表示識別碼為運算式評估工具的變數。 如需詳細資訊，請參閱[識別碼 &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)。  
  
## <a name="literals"></a>常值  
 運算式可以包含數值、字串及布林常值。 運算式中使用的字串常值必須加上引號。 數值和布林常值則不使用引號。 運算式語言包括常逸出之字元的逸出序列。 如需詳細資訊，請參閱[常值 &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md)。  
  
## <a name="operators"></a>運算子  
 運算式評估工具包含一組運算子，提供與 Transact-SQL、C++ 和 C# 語言中運算子類似的功能。 不過，運算式語言還包括額外的運算子，並且使用您可能不熟悉的不同符號。 如需詳細資訊，請參閱[運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)。  
  
### <a name="namespace-resolution-operator"></a>命名空間解析運算子  
 運算式使用命名空間解析運算子 (::) 使相同名稱的變數意義明確。 藉由使用命名空間解析運算子，您可以利用變數的命名空間限定變數，如此即可在封裝中使用多個相同名稱的變數。  
  
#### <a name="cast-operator"></a>轉換運算子  
 轉換運算子會將運算式結果、資料行值、變數值以及常數從一種資料類型轉換為另一種。 運算式語言提供的轉換運算子與 C 和 C# 語言提供的轉換運算子類似。 在 Transact-SQL 中，CAST 和 CONVERT 函數即提供此功能。 轉換運算子的語法與 CAST 和 CONVERT 所使用的語法不同之處如下：  
  
-   它可使用運算式作為引數。  
  
-   其語法不包括 CAST 關鍵字。  
  
-   其語法不包括 AS 關鍵字。  
  
##### <a name="conditional-operator"></a>條件運算子  
 條件運算子會根據布林運算式的評估，傳回兩種運算式的其中一種。 運算式語言提供的條件運算子與 C 和 C# 語言提供的條件運算子類似。 在多維度運算式 (MDX) 中，IIF 函數即提供類似的功能。  
  
###### <a name="logical-operators"></a>邏輯運算子  
 運算式語言支援邏輯 NOT 運算子所使用的 ! 字元。 在 Transact-SQL 中，! 運算子內建在一組關係運算子中。 例如，Transact-SQL 提供 > 和 !> 運算子。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 運算式語言不支援 ! 運算子和其他 運算子的組合。 例如，將 ! 和 > 結合至 !> 則 無效。 不過，針對不等於 (not-equal-to) 比較，運算式語言支援內建的 != 字元組合。  
  
###### <a name="equality-operators"></a>相等運算子  
 運算式評估工具文法描述提供 == 相等運算子。 此運算子相當於 Transact-SQL 中的 = 運算子以及 C# 中的 == 運算子。  
  
## <a name="functions"></a>函數  
 運算式語言包括與 Transact-SQL 函數和 C# 方法類似的日期和時間函數、數學函數以及字串函數。  
  
 其中有少數函數的名稱與 Transact-SQL 函數相同，但是在運算式評估工具中其功能則稍有不同。  
  
-   在 Transact-SQL 中，ISNULL 函數會以指定的值取代 Null 值，而運算式評估工具 ISNULL 函數則根據運算式是否為 Null 傳回布林。  
  
-   在 Transact-SQL 中，ROUND 函數包括截斷結果集的選項，而運算式評估工具 ROUND 函數則沒有。  
  
 如需詳細資訊，請參閱[函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)。  
  
## <a name="related-tasks"></a>相關工作  
 [在資料流程元件中使用運算式](http://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>相關內容  
  
-   pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](http://go.microsoft.com/fwlink/?LinkId=746575)  
  
-   social.technet.microsoft.com 上的技術文件： [SSIS 運算式範例](http://go.microsoft.com/fwlink/?LinkId=220761)  
  
  
