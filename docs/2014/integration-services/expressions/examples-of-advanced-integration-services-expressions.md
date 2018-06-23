---
title: 進階 Integration Services 運算式範例 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- functions [Integration Services]
- operators [Integration Services]
- expressions [Integration Services], examples
- examples [Integration Services]
ms.assetid: c7794ba3-0de5-466b-ae8a-9ddd27360049
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8ce3f4c37d7c590166beb53879c624ae70d9a3e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034170"
---
# <a name="examples-of-advanced-integration-services-expressions"></a>進階 Integration Services 運算式範例
  本節提供組合多個運算子和函數的進階運算式範例。 如果在優先順序條件約束或「條件式分割」轉換中使用運算式，則評估結果必須為布林。 不過，該條件約束不會套用至屬性運算式、變數、「衍生的資料行」轉換，或「For 迴圈」容器中使用的運算式。  
  
 下列範例使用 **AdventureWorks** 和 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 各範例代表其使用的資料表。  
  
## <a name="boolean-expressions"></a>布林運算式  
  
-   這個範例使用 **Product** 資料表。 運算式會評估 **SellStartDate** 資料行中的月份項目，而如果月份為六月或更晚的月份，則傳回 TRUE。  
  
    ```  
    DATEPART("mm",SellStartDate) > 6  
    ```  
  
-   這個範例使用 **Product** 資料表。 運算式會評估 **ListPrice** 資料行除以 **StandardCost** 資料行的進位結果，而如果結果大於 1.5，則傳回 TRUE。  
  
    ```  
    ROUND(ListPrice / StandardCost,2) > 1.50  
    ```  
  
-   這個範例使用 **Product** 資料表。 如果三項運算的評估結果均為 TRUE，則運算式會傳回 TRUE。 如果 **Size** 資料行和 **BikeSize** 變數的資料類型不相容，則運算式需要明確轉換，如第二個範例所示。 轉換為 DT_WSTR 包括字串長度。  
  
    ```  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE && Size != @BikeSize  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE  && Size != (DT_WSTR,10)@BikeSize  
    ```  
  
-   此範例使用 **CurrencyRate** 資料表。 運算式會比較資料表中和變數的值。 如果 **FromCurrencyCode** 或 **ToCurrencyCode** 資料行中的項目等於變數值，且 **AverageRate** 中的值大於 **EndOfDayRate**中的值，則會傳回 TRUE。  
  
    ```  
    (FromCurrencyCode == @FromCur || ToCurrencyCode == @ToCur) && AverageRate > EndOfDayRate  
    ```  
  
-   此範例使用 **Currency** 資料表。 如果 **Name** 中的第一個字元不是 a 或 A，則運算式會傳回 TRUE。  
  
    ```  
    SUBSTRING(UPPER(Name),1,1) != "A"  
    ```  
  
     下列運算式提供相同的結果，但更有效率，因為只會將一個字元轉換成大寫。  
  
    ```  
    UPPER(SUBSTRING(Name,1,1)) != "A"  
    ```  
  
## <a name="non-boolean-expressions"></a>非布林運算式  
 非布林運算式可用於「衍生的資料行」轉換、屬性運算式，以及「For 迴圈」容器。  
  
-   這個範例使用 **Contact** 資料表。 運算式會移除 **FirstName**、 **MiddleName**和 **LastName** 資料行中開頭和尾端的空格。 如果不是 Null，則會擷取 **MiddleName** 資料行的第一個字母、串連中間的縮寫與 **FirstName** 和 **LastName**中的值，以及在各值之間插入適當的空格。  
  
    ```  
    TRIM(FirstName) + " " + (!ISNULL(MiddleName) ? SUBSTRING(MiddleName,1,1) + " " : "") + TRIM(LastName)  
    ```  
  
-   這個範例使用 **Contact** 資料表。 運算式會驗證 **Salutation** 資料行中的項目。 它會傳回 **Salutation** 項目或空白字串。  
  
    ```  
    (Salutation == "Sr." || Salutation == "Ms." || Salutation == "Sra." || Salutation == "Mr.") ? Salutation : ""  
    ```  
  
-   這個範例使用 **Product** 資料表。 運算式會將 **Color** 資料行中的第一個字元轉換成大寫，並將其餘字元轉換成小寫。  
  
    ```  
    UPPER(SUBSTRING(Color,1,1)) + LOWER(SUBSTRING(Color,2,15))  
    ```  
  
-   這個範例使用 **Product** 資料表。 運算式會計算產品售出的月數，而且如果 **SellStartDate** 或 **SellEndDate** 資料行包含 NULL，則會傳回「Unknown」字串。  
  
    ```  
    !(ISNULL(SellStartDate)) && !(ISNULL(SellEndDate)) ? (DT_WSTR,2)DATEDIFF("mm",SellStartDate,SellEndDate) : "Unknown"  
    ```  
  
-   這個範例使用 **Product** 資料表。 運算式會計算 **StandardCost** 資料行上的標記，並將結果進位至兩位有效位數。 此結果會以百分比表示。  
  
    ```  
    ROUND(ListPrice / StandardCost,2) * 100  
    ```  
  
## <a name="related-tasks"></a>相關工作  
 [在資料流程元件中使用運算式](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
 pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](http://pragmaticworks.com/cheatsheet/)  
  
  