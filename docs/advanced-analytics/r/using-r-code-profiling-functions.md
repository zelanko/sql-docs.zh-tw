---
title: 使用 R 程式碼剖析函式
description: 使用 R 程式碼剖析函式來傳回內部函式呼叫的相關資訊, 以改善效能並在 SQL Server 上取得 R 計算的更快結果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e03ae1a8c4cdab87f46f63da6271886b4518b5e3
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715009"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>使用 R 程式碼剖析功能來改善效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

除了使用 SQL Server 資源和工具來監視 R 指令碼執行之外，您還可以使用由其他 R 套件提供的效能工具，來取得內部函式呼叫的相關詳細資訊。 

> [!TIP]
> 本文提供基本資源説明您開始使用。 如需專家指引, 建議您[Hadley wickham 針對的「Advanced R](http://adv-r.had.co.nz)」中的*Performance*區段。

## <a name="using-rprof"></a>使用 RPROF

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof)是基底封裝[**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1)中包含的函式, 預設會載入此功能。 

一般而言，*rprof* 函式的運作方式，是在指定的時間間隔將呼叫堆疊寫出至檔案。 接著, 您可以使用[*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof)函式來處理輸出檔案。 *rprof* 的其中一個優點，在於它會執行取樣，因此降低監視的效能負擔。

若要在您的程式碼中使用 R 程式碼剖析，您必須呼叫此函式並指定其參數，包含將寫入之記錄檔的位置名稱。 程式碼剖析可在您的程式碼中開啟或關閉。 下列語法說明基本用法: 

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

Microsoft R Open 的檔 (預設會安裝) 包含手動開發 R 語言的擴充功能, 以詳細討論[分析和調試](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)程式。 您可以在 C:\Program Files\Microsoft SQL Server\MSSQL13. 的電腦上找到相同的檔MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>另請參閱

+ [utils R 封裝](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ [「Advanced R」 by Hadley Wickham 針對](http://adv-r.had.co.nz)
