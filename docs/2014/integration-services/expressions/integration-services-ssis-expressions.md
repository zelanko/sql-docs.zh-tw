---
title: Integration Services (SSIS) 運算式 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- expressions [Integration Services], packages
- SSIS packages, expressions
ms.assetid: 26d2e242-7f60-4fa9-a70d-548a80eee667
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 489fad24cb8b62a11aca1914d0c5b24f180d5234
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428505"
---
# <a name="integration-services-ssis-expressions"></a>Integration Services (SSIS) 運算式
  運算式是產生單一資料值的符號組合 (識別碼、常值、函數和運算子)。 簡單的運算式可以是單一常數、變數或函數。 通常運算式都比較複雜，更常使用多個運算子和函數，並參考多個資料行和變數。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，運算式可用於定義 CASE 陳述式的條件、建立和更新資料行中的值、指派值到變數、在執行階段更新或擴展屬性、定義優先順序條件約束中的條件約束和提供「For 迴圈」容器所使用的運算式。  
  
 運算式以運算式語言和運算式評估工具為基礎。 運算式評估工具會剖析運算式，並判斷運算式是否遵循運算式語言的規則。 如需有關運算式語法以及支援的常值和識別碼的詳細資訊，請參閱下列主題。  
  
-   [語法 &#40;SSIS&#41;](syntax-ssis.md)  
  
-   [常值 &#40;SSIS&#41;](numeric-string-and-boolean-literals.md)  
  
-   [識別項 &#40;SSIS&#41;](identifiers-ssis.md)  
  
## <a name="components-that-use-expressions"></a>使用運算式的元件  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的下列元素可使用運算式：  
  
-   「條件式分割」轉換是以運算式為基礎，實作決策結構以將資料列導向不同的目的地。 「條件式分割」轉換中使用的運算式必須評估為 `true` 或 `false`。 例如，可以將運算式 "Column1 > Column2" 中符合條件的資料列傳送至不同的輸出。  
  
-   「衍生的資料行」轉換會利用透過使用擴展資料流程中新資料行或更新現有資料行之運算式所建立的值。 例如，運算式 Column1 + " ABC" 可用於更新值或建立具有串連字串的新值。  
  
-   變數會使用運算式來設定其值。 例如，GETDATE() 會將變數值設為目前的日期。  
  
-   優先順序條件約束可使用運算式，指定決定受條件約束的工作或封裝中的容器是否執行的條件。 優先順序條件約束中使用的運算式必須評估為 `true` 或 `false`。 例如，運算式 \@A > \@B 將兩個使用者定義變數進行比較，以決定受條件約束的工作是否執行。  
  
-   「For 迴圈」容器可使用運算式建立迴圈結果使用的初始化、評估和累加陳述式。 例如，運算式 \@Counter = 1 會初始化迴圈計數器。  
  
 運算式還可用於更新封裝、容器 (例如「For 迴圈」和「Foreach 迴圈」)、工作、封裝和專案層級之連接管理員、記錄提供者和 Foreach 列舉值的屬性值。 例如，使用屬性運算式，可將字串 "Localhost.AdventureWorks" 指派到「執行 SQL」工作的 ConnectionName 屬性。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](use-property-expressions-in-packages.md)。  
  
## <a name="icon-markers-for-expressions"></a>運算式的圖示標記  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，已經設定運算式的連接管理員、變數和工作旁，會顯示一個特殊的圖示標記。 所有支援運算式的 SSIS 物件，都可以使用 **HasExpressions** 屬性，但不包括變數。 這個屬性可讓您輕易地識別哪些物件具有運算式。  
  
## <a name="expression-builder"></a>運算式產生器  
 運算式產生器是可以用於建立運算式的圖形工具。 其位於 **[條件式分割轉換編輯器]** 、 **[衍生的資料行轉換編輯器]** 對話方塊及 **[運算式產生器]** 對話方塊中，是可以用於建立運算式的圖形工具。  
  
 運算式產生器會提供包含封裝特定之元素的資料夾和包含運算式語言所提供之函數、類型轉換和運算子的資料夾。 封裝特定的元素包括系統變數和使用者自訂變數。 在 **[條件式分割轉換編輯器]** 和 **[衍生的資料行轉換編輯器]** 對話方塊中，還可以檢視資料行。 若要建立轉換的運算式，可以將項目從資料夾拖曳至 **[條件]** 或 **[運算式]** 資料行，或直接在資料行中輸入運算式。 運算式產生器會自動加入必要的語法元素，例如變數名稱的前置詞 \@。  
  
> [!NOTE]  
>  使用者定義變數和系統變數的名稱會區分大小寫。  
  
 變數有範圍，並且運算式產生器中的 **[Variables]** 資料夾只會列出處於範圍中的可用變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)。  
  
## <a name="related-tasks"></a>相關工作  
 [在資料流程元件中使用運算式](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
 social.technet.microsoft.com 上的技術文件： [SSIS 運算式範例](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
