---
title: "使用 R 程式碼分析函式 | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 132db249-b9f1-48f5-a63e-c9806cacc4af
caps.latest.revision: 6
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# 使用 R 程式碼分析函式
除了使用 SQL Server 資源和工具來監視執行 R 指令碼，您可以使用其他 R 封裝所提供的效能工具，以取得有關內部函式呼叫的詳細資訊。 本主題提供一些基本的資源，協助您開始的清單。 專家的指導，我們建議本章上 [效能](http://adv-r.had.co.nz/Performance.html) 書 」 「 進階 R"」，Hadley Wickham 所著書籍中。

## <a name="using-rprof"></a>使用 RPROF

*rprof* 是函式的基底的封裝中包含 **utils**, ，預設會載入哪些。 其中一個優點 *rprof* 是它會執行取樣，因而降低在監視的效能負擔。

若要使用 R 程式碼剖析程式碼中，您可以呼叫此函式，並指定它的參數，包括可供寫入記錄檔的位置的名稱。 請參閱說明 *rprof* 如需詳細資訊。

一般而言， *rprof* 函數寫出至檔案，在指定時間間隔的呼叫堆疊的運作。 然後您可以使用 *summaryRprof* 函數來處理輸出檔。 

程式碼剖析可開啟和關閉程式碼中。 若要開啟程式碼剖析、 暫停程式碼剖析，並再重新啟動，您會使用一連串的呼叫 *rprof*:

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


> [!NOTE] 使用此函式需要在執行程式碼的電腦上安裝的 Windows Perl。 因此，我們建議您在 R 環境中，在開發期間分析程式碼，然後將偵錯的程式碼部署到 SQL Server。  


## <a name="r-system-functions"></a>R 系統函數

R 語言包含許多的基底封裝函式傳回系統變數的內容。 

例如，R 程式碼的一部分，您可以使用 `Sys.timezone` 取得目前時區或 `Sys.Time` 取得系統時間 

若要取得個別 R 系統函數的相關資訊，請輸入函數名稱為 R 的引數 `help()` R 的命令提示字元的函式。

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>偵錯和使用程式碼剖析

Microsoft R Open，預設安裝的文件包含的手冊，以開發程式碼剖析和偵錯的詳細討論的 R 語言擴充功能。

本章也會提供線上︰ [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>R 的說明檔的位置

C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\doc\manual


