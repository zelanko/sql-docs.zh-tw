---
title: 使用 R 程式碼分析函式來改善效能
description: 使用 R 分析函式來收集實用的資訊，以改善效能，並在 SQL Server 上更快取得 R 計算的結果。 *rprof* 函式會收集並傳回內部函式呼叫的相關資訊。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/30/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 53c3e7f55fa21d033bfda3f2e660bd1b9a92991f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470739"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>使用 R 分析函式來改善效能
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

此文章描述由 R 套件所提供的效能工具，以取得內部函式呼叫的相關資訊。 您可以使用此資訊來改善程式碼效能。

> [!TIP]
> 本文提供您開始使用時的基本資源。 如需專家指導，建議您閱讀 [由 Hadley Wickham 所著 "Advanced R"](http://adv-r.had.co.nz) 中的 *Performance* 一節。

## <a name="using-rprof"></a>使用 RPROF

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) 是包含在基底套件 [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1) 中的函式，預設會載入此函式。 

一般而言，*rprof* 函式的運作方式，是在指定的時間間隔將呼叫堆疊寫出至檔案。 然後，您可以使用 [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) 函式來處理輸出檔案。 *rprof* 的其中一個優點，在於它會執行取樣，因此降低監視的效能負擔。

若要在您的程式碼中使用 R 程式碼剖析，您必須呼叫此函式並指定其參數，包含將寫入之記錄檔的位置名稱。 程式碼剖析可在您的程式碼中開啟或關閉。 下列語法說明基本用法： 

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

Microsoft R Open 的文件 (預設會安裝) 包含開發 R 語言延伸模組的手冊，其中會詳細討論[分析與偵錯](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)。

## <a name="next-steps"></a>後續步驟

+ 如需在 SQL Server 中將 R 指令碼最佳化的詳細資訊，請參閱[適用於 R 的效能微調及資料最佳化](r-and-data-optimization-r-services.md)。
+ 如需 SQL Server 上效能微調的更完整資訊，請參閱 [SQL Server 資料庫引擎和 Azure SQL Database 的效能中心](/sql/relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database)。
+ 如需 utils 套件的詳細資訊，請參閱 [R Utils 套件](https://www.rdocumentation.org/packages/utils/versions/3.5.1) \(英文\)。
+ 如需 R 程式設計的深入討論，請參閱 [Hadley Wickham 所撰寫的＜進階 R＞](http://adv-r.had.co.nz) \(英文\)。
