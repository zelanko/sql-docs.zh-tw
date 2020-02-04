---
title: 為資料整頓工作產生程式碼
titleSuffix: Azure Data Studio
description: 本文說明如何使用 Azure Data Studio 中的 PROSE Code Accelerator，為常見的資料整頓工作自動產生程式碼。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e21c172bf886695a3d424d25907a0c36e4b22f20
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67957689"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>使用 PROSE Code Accelerator 進行資料整頓

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

PROSE Code Accelerator 會為您的資料整頓工作產生可讀取的 Python 程式碼。 當您在 Azure Data Studio 的筆記本中工作時，您可以順暢地將產生的程式碼與手寫的程式碼融合在一起。 本文提供如何使用 Code Accelerator 的概觀。

 > [!NOTE]
 > Program Synthesis using Examples (也稱為 PROSE) 是一項 Microsoft 技術，使用 AI 產出人們看得懂的程式碼。 該技術會去分析使用者的意圖和資料、產出數個候選程式，然後透過排名演算法挑選最佳程式。 若要深入了解 PROSE 技術，請瀏覽 [PROSE 首頁](https://microsoft.github.io/prose/)。

Code Accelerator 會隨 Azure Data Studio 預先安裝。 您可以把它匯入筆記本，就像其他 Python 套件一樣。 依照慣例，我們會以 cx (簡稱) 匯入。

```python
import prose.codeaccelerator as cx
```

在目前版本中，Code Accelerator 可以針對下列工作以智慧方式產生 Python 程式碼：

- 將資料檔案讀入 Pandas 或 Pyspark 資料框架。
- 修正資料框架中的資料類型。
- 在字串清單中尋找呈現出模式的規則運算式。

若要取得 Code Accelerator 方法的一般概觀，請參閱[文件](https://aka.ms/prose-codeaccelerator-overview)。

## <a name="reading-data-from-a-file-to-a-dataframe"></a>將檔案中的資料讀入資料框架

將檔案讀入資料框架通常涉及查看檔案的內容，並判斷要傳遞至資料載入程式庫的正確參數。 視檔案的複雜度而定，識別正確的參數可能需要反覆查看多次。

PROSE Code Accelerator 藉由分析資料檔案的結構，然後自動產出程式碼以載入檔案，來解決此問題。 在大多數情況下，產出的程式碼可以正確地剖析資料。 在少數情況下，您可能需要調整程式碼以符合您的需求。

請考慮下列範例：

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

上述程式碼區塊會列印下列 Python 程式碼來讀取分隔檔。 注意 PROSE 如何自動找出要略過的行數、標頭、引號字元、分隔符號等。

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

Code Accelerator 可以產出程式碼，將分隔、JSON 和固定寬度的檔案載入資料框架。 若要讀取固定寬度的檔案，`ReadFwfBuilder` 會選擇性地採用人們看得懂的結構描述檔案，以便進行剖析來取得資料行位置。 若要深入了解，請參閱[文件](https://aka.ms/prose-codeaccelerator-docs)。

## <a name="fixing-data-types-in-a-dataframe"></a>修正資料框架中的資料類型

Pandas 或 Pyspark 資料框架經常會出現錯誤資料類型。 這通常是因為資料行中有幾項不合格的值所造成。 因此，整數會解讀為浮點數或字串，而日期會解讀為字串。 手動修正資料類型所花費的心力會與資料行數目成正比。

您可以在這些情況下使用 `DetectTypesBuilder` 方法。 它會分析資料，並產出程式碼來修正資料類型，而不是以黑箱方式修正資料類型。 此程式碼可作為起點。 您可以視需要檢閱、使用或修改。

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

若要深入了解，請參閱[文件](https://aka.ms/prose-codeaccelerator-fixtypes)。

## <a name="identifying-patterns-in-strings"></a>識別字串中的模式

另一個常見的案例是在字串資料行中偵測模式，以便清除或分組。 例如，您可能有一個日期資料行，其中包含多種不同格式的日期。 若要將值標準化，您可能需要使用規則運算式來撰寫條件陳述式。


|   |名稱                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-Apr-67      |
| 4 |Maya de Villiers          |19-Mar-60      |

視資料的數量和多樣性而定，針對資料行裡不同的模式撰寫規則運算式會是非常耗時的工作。 `FindPatternsBuilder` 是功能強大的程式碼加速工具，藉由為字串清單產出規則運算式來解決上述問題。

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

以下是 `FindPatternsBuilder` 為上述資料所產出的規則運算式。

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

除了產出規則運算式之外，`FindPatternsBuilder` 也可以產出程式碼，以根據產生的 RegEx 將值叢集化。 它也可以宣告資料行中的所有值都符合產出的規則運算式。 若要深入了解並查看其他實用案例，請參閱[文件](https://aka.ms/prose-codeaccelerator-findpatterns)。
