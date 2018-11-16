---
title: 使用 R 程式碼剖析函式 （SQL Server 機器學習服務） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 64f065df5f5769e37bb1d5a8dbc2fba2d5f936ee
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703966"
---
# <a name="using-r-code-profiling-functions"></a>使用 R 程式碼剖析函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

除了使用 SQL Server 資源和工具來監視 R 指令碼執行之外，您還可以使用由其他 R 套件提供的效能工具，來取得內部函式呼叫的相關詳細資訊。 本主題提供一些基本資源的清單，以協助您開始。 如需專家指導，我們建議上一章[效能](https://adv-r.had.co.nz/Performance.html)書 《 進階 R，Hadley Wickham 所著中。

## <a name="using-rprof"></a>使用 RPROF

*rprof* 是包含在基底套件 **utils** 中的函式，預設會載入此函式。 *rprof* 的其中一個優點，在於它會執行取樣，因此降低監視的效能負擔。

若要在您的程式碼中使用 R 程式碼剖析，您必須呼叫此函式並指定其參數，包含將寫入之記錄檔的位置名稱。 如需詳細資料，請參閱 *rprof* 的說明。

一般而言，*rprof* 函式的運作方式，是在指定的時間間隔將呼叫堆疊寫出至檔案。 然後您可以使用 *summaryRprof* 函式來處理輸出檔。 

程式碼剖析可在您的程式碼中開啟或關閉。 若要開啟程式碼剖析，請暫停程式碼剖析，然後重新啟動它，您將會使用一連串針對 *rprof* 的呼叫：

1. 指定程式碼剖析輸出檔。

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. 關閉程式碼剖析
    ```R
    Rprof(NULL)
    ```
    
3. 重新啟動程式碼剖析
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE]
> 若要使用此函式，必須在執行程式碼的電腦上安裝 Windows Perl。 因此，建議您在 R 環境中於開發期間對程式碼進行剖析，然後將已偵錯的程式碼部署到 SQL Server。  


## <a name="r-system-functions"></a>R 系統函式

R 語言包含許多針對傳回系統變數內容的基底套件函式。 

例如，做為您 R 程式碼的一部分，您可能會使用 `Sys.timezone` 來取得目前時區，或是使用 `Sys.Time` 來從 R 取得系統時間。 

若要取得個別 R 系統函式的相關資訊，請從 R 命令提示字元輸入函式名稱做為 R `help()` 函式的引數。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>在 R 中進行偵錯與程式碼剖析

Microsoft R Open 的文件 (預設會安裝) 包含開發適用於 R 語言之擴充功能的手冊，其中會詳細討論程式碼剖析與偵錯。

本章也會提供線上： [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>R 說明檔的位置

C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual



