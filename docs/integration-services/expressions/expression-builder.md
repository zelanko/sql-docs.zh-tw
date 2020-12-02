---
description: 運算式產生器
title: 運算式產生器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionbuilder.f1
helpviewer_keywords:
- Expression Builder dialog box
ms.assetid: 4717ce33-bd4e-44bc-81e0-002de075b4d1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6f8eb6c6771e2684d03380a721c7ef96dcb08488
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123289"
---
# <a name="expression-builder"></a>運算式產生器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  使用 [運算式產生器] 對話方塊，即可藉由使用圖形化使用者介面列出變數以及提供函數的內建參考、類型轉換和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式語言所包含的運算子，來建立和編輯屬性運算式或撰寫可設定變數值的運算式。  
  
 屬性運算式是指派給屬性的運算式。 在評估運算式時，會動態更新屬性以使用運算式的評估結果。 同樣地，變數中所使用的運算式可使運算式的評估結果更新變數值。  
  
 有許多使用運算式的方法。  
  
-   **工作** 透過插入儲存在變數中的電子郵件地址，來更新「傳送郵件」工作所使用的「收件者」欄位；透過串連如 "Sales for:" 字串與 GETDATE 函數傳回的目前日期，來更新「主旨」欄位。  
  
-   **變數** 使用像 `DATEPART("mm",GETDATE())`之類的運算式來將變數的值設定為目前的月份；或是使用運算式 `"Today's date is " + (DT_WSTR,30)(GETDATE())`來串連字串常值和目前的日期，以設定字串值。  
  
-   **連接管理員** 使用含有不同字碼頁識別碼的變數來設定一般檔案連接管理員的字碼頁；或是在運算式中輸入如 3 的正整數，以指定資料檔中要跳過的資料列數。  
  
 若要深入了解屬性運算式以及撰寫運算式，請參閱[在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)和 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**變數**|展開 **[變數]** 資料夾，然後將變數拖曳至 **[運算式]** 方塊。|  
|**數學函式**<br /><br /> **字串函式**<br /><br /> **日期/時間函數**<br /><br /> **NULL 函數**<br /><br /> **類型轉換**<br /><br /> **運算子**|展開資料夾，然後將函數、類型轉換和運算子拖曳至 **[運算式]** 方塊。|  
|**運算式**|編輯或輸入運算式。|  
|**評估值**|列出運算式的評估結果。|  
|**評估運算式**|按一下 **[評估運算式]** ，即可檢視運算式的評估結果。|  
  
## <a name="see-also"></a>另請參閱  
 [運算式頁面](../../integration-services/expressions/expressions-page.md)   
 [屬性運算式編輯器](../../integration-services/expressions/property-expressions-editor.md)   
 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)   
 [系統變數](../../integration-services/system-variables.md)  
  
  
