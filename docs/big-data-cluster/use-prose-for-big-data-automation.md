---
title: 產生資料有爭議的工作程式的碼
titleSuffix: Azure Data Studio
description: 本文說明如何使用 Azure 資料 Studio 中的文字的程式碼加速器，自動產生程式碼的常見的資料有爭議的工作。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e21c172bf886695a3d424d25907a0c36e4b22f20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957689"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>使用文字程式碼加速器 data Wrangling

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

PROSE 程式碼加速器會產生可讀取的 Python 程式碼，以您的資料有爭議的工作。 在 Azure Data Studio 中的 notebook 中工作時，您可以無縫式的方式混合搭配您手動撰寫的程式碼產生的程式碼。 本文將概述如何使用程式碼的加速器。

 > [!NOTE]
 > 程式 Synthesis using Examples，也稱為 PROSE，是一種 Microsoft 技術，產生人類看得懂的程式碼使用 AI。 它會分析使用者的意圖，以及資料、 產生數個候選程式，並挑選最佳的計劃使用排名演算法。 若要深入了解 PROSE 技術，請造訪[PROSE 首頁](https://microsoft.github.io/prose/)。

程式碼 Accelerator 已預先安裝 Azure Data Studio。 您可以匯入類似在 notebook 中的其他 Python 套件。 依照慣例，我們它匯入為 cx 簡稱。

```python
import prose.codeaccelerator as cx
```

在目前的版本中，程式碼加速器以智慧方式可以產生 Python 程式碼來執行下列工作：

- 資料檔案讀取至 Pandas 或 Pyspark 資料框架。
- 修正資料框架中的資料類型。
- 尋找規則運算式，表示字串清單中的模式。

若要取得程式碼加速器方法的一般概觀，請參閱[文件](https://aka.ms/prose-codeaccelerator-overview)。

## <a name="reading-data-from-a-file-to-a-dataframe"></a>從檔案讀取資料的資料框架

通常，讀取檔案的資料框架牽涉到查看檔案的內容，並判斷正確的參數，將資料載入程式庫。 根據檔案的複雜度，找出正確的參數可能需要數個反覆項目。

PROSE 程式碼加速器會解決此問題，分析資料檔案的結構，並自動產生程式碼載入檔案。 在大部分情況下，產生的程式碼會正確地剖析資料。 在少數情況下，您可能需要調整以符合您需求的程式碼。

參考下列範例：

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

先前的程式碼區塊會列印下列 python 程式碼，讀取分隔的檔案。 請注意如何 PROSE 會自動找出要跳過，標頭、 quotechars、 分隔符號等等的行數。

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

程式碼加速器可以產生程式碼，以分隔的負載、 JSON 和固定寬度檔案的資料框架。 用於讀取固定寬度檔案`ReadFwfBuilder`會選擇性使用人類看得懂的結構描述檔案，它可以剖析來取得資料行位置。 若要進一步了解，請參閱[文件](https://aka.ms/prose-codeaccelerator-docs)。

## <a name="fixing-data-types-in-a-dataframe"></a>修正資料框架中的資料類型

通常會有 pandas 或含有錯誤的資料類型的 pyspark 資料框架。 這是因為幾個不合格的情況下，資料行的值。 如此一來，整數會讀取為浮點數或字串和日期會讀取為字串。 若要手動修正資料類型所需的工作的資料行數目成正比。

您可以使用`DetectTypesBuilder`在這些情況下。 它會分析資料和而不是黑色方塊的方式修正資料型別，它會產生程式碼以修正資料型別。 程式碼做為起點。 您可以檢視、 使用，或視需要修改它。

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

若要進一步了解，請參閱[文件](https://aka.ms/prose-codeaccelerator-fixtypes)。

## <a name="identifying-patterns-in-strings"></a>識別字串中的模式

偵測模式中的字串資料行，以便清除或分組為另一個常見案例。 比方說，您可能將日期的日期資料行在多個不同的格式。 為了標準化值，您可能想要撰寫使用規則運算式的條件陳述式。


|   |名稱                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-Apr-67      |
| 4 |Maya de Villiers          |19-3 月-60      |

根據磁碟區和資料的多樣性，撰寫資料行中的不同模式的規則運算式可能會相當耗時的工作。 `FindPatternsBuilder`是功能強大的程式碼加速的一項工具，可解決上述問題，藉由產生的字串的規則運算式的清單。

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

以下是所產生的規則運算式`FindPatternsBuilder`上述的資料。

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

除了產生規則運算式，`FindPatternsBuilder`也可以產生程式碼叢集根據產生的 regex 的值。 此外，它也可以判斷提示的資料行中的所有值都符合產生的規則運算式。 若要進一步了解，並查看其他有用的案例，請參閱[文件](https://aka.ms/prose-codeaccelerator-findpatterns)。
