---
title: "ScaleR 函式，以使用 SQL Server 資料 | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# ScaleR 函式，以使用 SQL Server 資料
本主題提供搭配使用 SQL Server，以及在語法上的註解的主要 ScaleR 函式的概觀。

ScaleR 函式和使用方式的完整清單，請參閱 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/index#) MSDN library 中的參考。 

## 使用 SQL Server 資料來源的函式
下列函式可讓您定義 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料來源。 資料來源物件是指定的連接字串，以及您想要定義為資料表、 檢視或查詢的資料集的容器。 不支援預存程序呼叫。  

除了定義資料來源，您可以從 R 執行 DDL 陳述式，如果您有執行個體和資料庫的必要權限。 
+ [RxSqlServerData](https://msdn.microsoft.com/microsoft-r/scaler/RxSqlServerData) -定義 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料來源物件
+ [rxSqlServerDropTable](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerDropTable) -卸除 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料表
+ [rxSqlServerTableExists](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerTableExists) -檢查資料庫資料表或物件存在
+ [rxExecuteSQLDDL](https://msdn.microsoft.com/microsoft-r/scaler/rxExecuteSQLDDL) -執行命令來定義、 管理或控制 SQL 資料，但不是會傳回資料  

## 函式來定義或管理計算內容
下列函式可讓您定義新的計算內容、 切換計算內容，或識別目前的計算內容。
+ [RxComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/RxComputeContext) -建立計算的內容。 
+ [rxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxInSqlServer) -產生 SQL Server 的計算內容，讓 **ScaleR** 函式執行 SQL Server R Services 中。
+ [rxGetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxGetComputeContext) -取得目前的計算內容。 
+ [rxSetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxSetComputeContext) -指定哪些計算要使用內容。 

## 使用資料來源的函式
建立資料來源物件之後，您可以開啟，以取得資料，或寫入新的資料。 根據資料來源中的大小，也可以定義的批次大小做為資料來源的一部分並且移動區塊 （chunk） 中的資料。 
+ [rxIsOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxIsOpen) -請檢查是否有可用資料來源
+ [rxOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxOpen) -開啟用於讀取的資料來源
+ [rxReadNext](https://msdn.microsoft.com/microsoft-r/scaler/rxReadNext) -從來源讀取資料
+ [rxWriteNext](https://msdn.microsoft.com/microsoft-r/scaler/rxWriteNext) -將資料寫入至目標
+ [rxClose](https://msdn.microsoft.com/microsoft-r/scaler/rxclose) -關閉 [資料來源

如需使用這些 ScaleR 函式的詳細資訊，這可以使用資料來源以外 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，請參閱 [ Microsoft R Server-入門](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started)。

## 使用 XDF 檔案的函式
下列函數可用來建立本機資料快取 XDF 格式。 使用更多的資料，比可以傳輸，從資料庫中一個批次或超過記憶體內可容納的資料時，這個檔案可以是很有用。

如果定期在資料庫的本機工作站之間移動大量資料，而不是查詢資料庫中重複的每個 R 作業，您可以使用 XDF 檔案儲存在本機的資料，並使用該 R 工作區中使用 XDF 檔案做為快取。

+ `rxImport` XDF 檔從 ODBC 來源移動資料
+ `RxXdfData` -建立 XDF 資料物件
+ `RxDataStep` -讀取資料 XDF int 資料框架
+ `rxXdfToDataFrame` -從資料讀入 XDF 資料框架
+ `rxReadXdf` -會將資料從 XDF 讀入資料框架

如需如何使用 XDF 檔案的範例，請參閱本教學課程︰  [資料科學深入探討-使用 ScaleR 函式](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)

如需有關這些 ScaleR 函式，可用於許多不同來源中的資料傳送，請參閱[ Microsoft R Server-入門](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started)。

## 另請參閱
[基底 R 和 ScaleR 函式的比較](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)
