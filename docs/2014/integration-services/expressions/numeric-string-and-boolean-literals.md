---
title: 常值 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- string literals
- numeric literals [Integration Services]
- Boolean literals
- expressions [Integration Services], literals
- literals [Integration Services]
- mapping literals [Integration Services]
ms.assetid: a980cd52-54ef-4b9c-b00c-e6807cf8e01f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9b307c48da04e32691afa12ff1b05f6a4e8c33d8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62897462"
---
# <a name="literals-ssis"></a>常值 (SSIS)
  運算式可以包含數值、字串及布林常值。 運算式評估工具支援各種不同的數值常值，例如整數、小數以及浮點常數。 運算式評估工具亦支援長尾碼和浮點尾碼，其指定運算式評估工具處理值的方式，以及數值常值中的科學記號。  
  
## <a name="numeric-literals"></a>數值常值  
 運算式評估工具支援整數和非整數的數值資料類型。 它還支援歷程識別碼，其為封裝元素的唯一數值識別碼。 歷程識別碼為數字，但無法在數學運算中使用。  
  
 運算式評估工具支援尾碼，可讓您用來指示運算式評估工具處理數值常值的方式。 例如，您可以寫入 37L 或 37l，指示將整數 37 視為長整數資料類型。  
  
 下表列出數值常值的後置詞。  
  
|後置詞|描述|  
|------------|-----------------|  
|L 或 l|長數值常值。|  
|U 或 u|不帶正負號的數值常值。|  
|E 或 e|科學記號中的指數。|  
  
 下表列出數值運算式元素及其規則運算式。  
  
|運算式元素|規則運算式|描述|  
|------------------------|------------------------|-----------------|  
|以 D 表示的位數。|[0-9]|任何位數。|  
|以 E 表示的科學記號。|[Ee][+-]?{D}+|大寫或小寫 e、選擇性的 + 或 -，以及 D 中定義的一或多個位數。|  
|以 IS 表示的整數尾碼。|(([lL]?[uU]?)&#124;([uU]?[lL]?))|選擇性地大寫或小寫 u 和 I，或 u 和 I 的組合。 U 或 u 表示不帶正負號的值。 L 或 I 表示長數值。|  
|以 FS 表示的浮點尾碼。|([f&#124;F]&#124;[l&#124;L])|大寫或小寫 f 或 I。 F 或 f 表示浮點值 (DT_R4 資料類型)。 L 或 I 表示長數值 (DT_R8 資料類型)。|  
|以 H 表示的十六進位數。|[a-fA-F0-9]|任何十六進位數。|  
  
 下表描述使用規則運算式語言的有效數值常值。  
  
|規則運算式|描述|  
|------------------------|-----------------|  
|{D}+{IS}|至少有一位數 (D) 的整數數值常值，以及選擇性的長尾碼和 (或)不帶正負號的尾碼 (IS)。  例如：457、785u、986L 和 7945ul。|  
|{D}+{E}{FS}|至少有一位數 (D) 的非整數數值常值、科學記號，以及長尾碼或浮點尾碼。  例如：4E8l、13e-2f 和 5E+L。|  
|{D}*"."{D}+{E}?{FS}|有小數位數的非整數數值常值、至少有一位數 (D) 的小數、選擇性的指數 (E)，以及一個浮點或一個長識別碼 (FS)。 這個數值常值的資料類型為 DT_R4 或 DT_R8。  例如：6.45E3f、.89E-2l 和 1.05E+7F。|  
|{D}+"."{D}*{E}?{FS}|至少有一個有效位數的非整數數值常值、小數位數、指數 (E)，以及一個浮點或一個長識別碼 (FS)。 這個數值常值的資料類型為 DT_R4 或 DT_R8。  例如：1.E-4f、4.6E6L 和 8.365E+2f。|  
|{D}*.{D}+|具有有效位數與小數位數的非整數數值常值。 它包含小數位數和至少一位數 (D) 的小數。 這個數值常值的資料類型為 DT_NUMERIC。  例如：.9、5.8 和 0.346。|  
|{D}+.{D}*|具有有效位數與小數位數的非整數數值常值。 它至少有一個有效位數 (D) 和一個小數位數。 這個數值常值的資料類型為 DT_NUMERIC。  例如：6.、0.2 和 8.0。|  
|#{D}+|歷程識別碼。 它是由井字號 (#) 字元和至少一位數 (D) 所組成。 例如：#123。|  
|0[xX]{H}+{uU}|十六進位格式的數值常值。 它包括零、大寫或小寫 x、至少一個大寫 H，以及選擇性的不帶正負號尾碼。 例如：0xFF0A 和 0X000010000U。|  
  
 如需運算式評估工具所使用之資料類型的詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
 運算式可包括不同資料類型的數值常數。 當運算式評估工具評估這些運算式時，會將資料轉換成相容的類型。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
 不過，某些資料類型之間的轉換需要明確轉換。 運算式評估工具會提供執行明確資料類型轉換的轉換運算子。 如需詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
### <a name="mapping-numeric-literals-to-integration-services-data-types"></a>將數值常數對應至 Integration Services 資料類型  
 運算式評估工具會在評估數值常值時執行下列轉換：  
  
-   整數數值常值會對應至整數資料類型，如下所示。  
  
    |後置詞|結果類型|  
    |------------|-----------------|  
    |None|DT_I4|  
    |U|DT_UI4|  
    |L|DT_I8|  
    |UL|DT_UI8|  
  
    > [!IMPORTANT]  
    >  如果缺少長 (L 或 l) 後置詞，運算式評估工具便會將帶正負號的值對應至 DT_I4 資料類型，以及將不帶正負號的值對應至 DT_UI4 資料類型，即使該值會讓資料類型溢位。  
  
-   包含指數的數值常值會轉換為 DT_R4 或 DT_R8 資料類型。 如果運算式包含長尾碼，則會轉換為 DT_R8；如果它包含浮點尾碼，則會轉換為 DT_R4 資料類型。  
  
-   如果非整數數值常值包含 F 或 f，則會對應至 DT_R4 資料類型。 如果它包含 L 或 l ，且數字為整數，則會對應至 DT_I8 資料類型。 如果它是實數，則會對應至 DT_R8 資料類型。 如果它包含長尾碼，則會轉換為 DT_R8 資料類型。  
  
-   含有效位數和小數位數的非整數數值常值會對應至 DT_NUMERIC 資料類型。  
  
## <a name="string-literals"></a>字串常值  
 字串常值必須以引號括住。 運算式語言針對常逸出的字元提供一組逸出序列，例如非列印字元和引號。  
  
 字串常值是由零或加上引號的多個字元所組成。 如果字串包含引號，則必須逸出，運算式才能進行剖析。 字串中允許任何雙位元組字元，但 \x0000 除外，因為 \x0000 字元是字串的 Null 終端子。  
  
 字串可包含其他需要逸出序列的字串。 下表列出字串常值的逸出序列。  
  
|逸出序列|描述|  
|---------------------|-----------------|  
|\a|警示|  
|\b|退格鍵|  
|\f|換頁字元|  
|\n|新行|  
|\r|歸位字元|  
|\t|水平 Tab 鍵|  
|\v|垂直 Tab 鍵|  
|\\"|引號|  
|\\\|反斜線|  
|\xhhhh|十六進位記號的 Unicode 字元|  
  
## <a name="boolean-literals"></a>布林常值  
 運算式評估工具可支援一般布林常值：`True` 和 `False`。 運算式評估工具不區分大小寫，並且允許使用任何大小寫字母的組合。 例如，TRUE 等於 True。  
  
> [!NOTE]  
>  在運算式中，布林常值必須以空格分隔。  
  
## <a name="related-content"></a>相關內容  
 pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet)  
  
  
