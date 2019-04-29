---
title: 衍生資料行轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntrans.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a2767de67eac1a0346f059e1a2c81a5698607dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900511"
---
# <a name="derived-column-transformation"></a>衍生的資料行轉換
  「衍生的資料行」轉換會將運算式套用至轉換輸入資料行，藉此建立新的資料行值。 運算式可包含來自轉換輸入之變數、函數、運算子和資料行的任意組合。 結果可加入做為新的資料行，或插入現有資料行做為取代值。 「衍生的資料行」轉換可定義多個衍生的資料行，且任何變數或輸入資料行都可在多個運算式中出現。  
  
 您可以使用此轉換執行下列工作：  
  
-   將不同資料行的資料串連至衍生的資料行中。 例如，您可以使用運算式 **，將** FirstName **和** LastName **資料行的值結合到名為**FullName `FirstName + " " + LastName`的單一衍生資料行中。  
  
-   使用如 SUBSTRING 的函數從字串資料擷取字元，然後將結果儲存到衍生的資料行中。 例如，您可以使用運算式 **，從** FirstName `SUBSTRING(FirstName,1,1)`資料行中擷取人員的名字縮寫。  
  
-   套用數學函數至數值資料，然後將結果儲存到衍生的資料行中。 例如，您可以使用運算式 **，將數值資料行**SalesTax `ROUND(SalesTax, 2)`的長度和有效位數變更為含有兩位小數的數字。  
  
-   建立比較輸入資料行和變數的運算式。 例如，您可以使用運算式 **，對照** ProductVersion **資料行中的資料比較變數**Version **，並根據比較結果，使用** Version **或**ProductVersion `ProductVersion == @Version? ProductVersion : @Version`的值。  
  
-   擷取日期時間值的部分。 例如，您可以使用運算式 `DATEPART("year",GETDATE())`，利用 GETDATE 和 DATEPART 函數擷取目前的年份。  
  
-   使用運算式將日期字串轉換成特定格式。  
  
## <a name="configuration-of-the-derived-column-transformation"></a>設定衍生資料行轉換  
 您可以利用下列方式設定「衍生的資料行」轉換：  
  
-   為每一個要變更的輸入資料行或新資料行提供運算式。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../expressions/integration-services-ssis-expressions.md)。  
  
    > [!NOTE]  
    >  如果運算式參考「衍生的資料行」轉換所覆寫的輸入資料行，則運算式會使用資料行的原始值，而非衍生的值。  
  
-   若要將結果加入新資料行，並且資料類型是 `string`，請指定字碼頁。 如需詳細資訊，請參閱 [Comparing String Data](../comparing-string-data.md)。  
  
 衍生的資料行轉換包括 FriendlyExpression 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../../expressions/use-property-expressions-in-packages.md)和 [轉換自訂屬性](transformation-custom-properties.md)。  
  
 這個轉換有一個輸入、一個規則輸出及一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [衍生的資料行轉換編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱[衍生的資料行轉換編輯器](../../derived-column-transformation-editor.md)。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用衍生的資料行轉換來衍生資料行值](derived-column-transformation.md)  
  
## <a name="related-content"></a>相關內容  
 social.technet.microsoft.com 上的技術文件： [SSIS 運算式範例](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
 部落格[如何使用 SSIS 分割資料行資料](https://microsoft-ssis.blogspot.com/2012/10/split-multi-value-column-into-multiple.html)。  
  
  
