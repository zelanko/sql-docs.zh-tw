---
title: "SQL Server R Services 效能微調 | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# SQL Server R Services 效能微調
[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 提供的平台，可開發展現全新深入見解的智慧型應用程式。 資料科學家可以使用 R 語言的能力，可訓練及使用資料儲存在內部建立模型 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 準備好開始生產模型之後，資料科學家可以使用資料庫管理員和 SQL 工程師部署在生產環境中的方案。 本節中的資訊提供高等級的指導方針調整這兩個效能時建立並定型模型，並將模型部署至實際執行時。

這份文件中的資訊假設您已熟悉 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 概念與術語。 一般 R 服務的詳細資訊，請參閱 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)。

> [!NOTE]
> 雖然大部分的這一節中的資訊設定的一般指引 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，某些資訊旨在 RevoScaleR 分析函式。

## 本節內容

* [SQL Server 組態](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)︰ 本文件提供指引，設定硬體， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 上已安裝。 它是最有用 __資料庫管理員__。

* [R 和資料最佳化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)︰ 本文件提供指引以 R 服務使用 R 指令碼。 它是最有用 __資料科學家__。

* [效能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)︰ 本文件提供測試資料以及 R 指令碼，可以用於測試上一個文件中提供的指導方針的影響。

## 參考

以下是此文件的開發中使用的資訊連結。

* [如何判斷適當的分頁檔大小為 64 位元版本的 Windows](https://support.microsoft.com/kb/2860880)

* [資料壓縮](../../relational-databases/data-compression/data-compression.md)

* [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [停用資料表或索引的壓縮](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

* [DISKSPD 存放負載產生器效能測試工具](https://github.com/microsoft/diskspd)

* [FSUtil 公用程式參考](https://technet.microsoft.com/library/cc753059.aspx)

* [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

* [R Services](../../advanced-analytics/r-services/r-services.md)

* [RxDForest 和 rxDTree 效能微調選項](https://support.microsoft.com/kb/3104235)

* [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)

* [RevoScaleR 使用者指南](https://packages.revolutionanalytics.com/doc/7.0.0/win/RevoScaleR_Users_Guide.pdf)

* [資源管理員](../../relational-databases/resource-governor/resource-governor.md)

## 另請參閱

 
 [R 服務的 SQL Server 組態](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [效能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 和資料最佳化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)