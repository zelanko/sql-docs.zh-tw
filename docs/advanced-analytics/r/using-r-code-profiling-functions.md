---
title: 使用 R 程式碼剖析函式-SQL Server Machine Learning 服務
description: 改善效能，並取得更快的結果，在 SQL Server 上的 R 計算，使用 R 程式碼剖析函式來傳回內部函式呼叫的相關資訊。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8d58125cc8e6ffe4378759d4ceb4bdd0354e2e6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962362"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>使用 R 程式碼剖析函式來改善效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

除了使用 SQL Server 資源和工具來監視 R 指令碼執行之外，您還可以使用由其他 R 套件提供的效能工具，來取得內部函式呼叫的相關詳細資訊。 

> [!TIP]
> 本文提供基本的資源，以協助您開始使用。 如需專家指導，我們建議您*效能*一節[Hadley Wickham 所著的 《 進階 R"](http://adv-r.had.co.nz)。

## <a name="using-rprof"></a>使用 RPROF

[*rprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof)是包含在基底套件函式[ **utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1)，根據預設，它會載入。 

一般而言，*rprof* 函式的運作方式，是在指定的時間間隔將呼叫堆疊寫出至檔案。 然後您可以使用[ *summaryRprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof)函式來處理輸出檔。 *rprof* 的其中一個優點，在於它會執行取樣，因此降低監視的效能負擔。

若要在您的程式碼中使用 R 程式碼剖析，您必須呼叫此函式並指定其參數，包含將寫入之記錄檔的位置名稱。 程式碼剖析可在您的程式碼中開啟或關閉。 下列語法會說明基本的使用方式： 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> 若要使用此函式，必須在執行程式碼的電腦上安裝 Windows Perl。 因此，建議您在 R 環境中於開發期間對程式碼進行剖析，然後將已偵錯的程式碼部署到 SQL Server。  


## <a name="r-system-functions"></a>R 系統函式

R 語言包含許多針對傳回系統變數內容的基底套件函式。 例如，做為您 R 程式碼的一部分，您可能會使用 `Sys.timezone` 來取得目前時區，或是使用 `Sys.Time` 來從 R 取得系統時間。 

若要取得個別 R 系統函式的相關資訊，請從 R 命令提示字元輸入函式名稱做為 R `help()` 函式的引數。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>在 R 中進行偵錯與程式碼剖析

Microsoft R Open，但預設安裝的文件包含開發討論的 R 語言擴充功能的手冊[分析和偵錯](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)在詳細資料。 您可以在 C:\Program Files\Microsoft SQL Server\MSSQL13 對電腦上找到的相同文件。MSSQLSERVER\R_SERVICES\doc\manual。

## <a name="see-also"></a>另請參閱

+ [utils R 套件](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ [Hadley Wickham 所著的 「 進階的 R"](http://adv-r.had.co.nz)
