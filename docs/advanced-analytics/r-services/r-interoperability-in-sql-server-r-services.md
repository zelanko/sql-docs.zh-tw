---
title: "在 SQL Server R Services R 互通性 | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 在 SQL Server R Services R 互通性

本主題著重於執行中的機制 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，並說明 Microsoft R 和開放原始碼 r 之間的差異其他元件的相關資訊，請參閱 [SQL Server 中的新元件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)。

### 開放原始碼 R 元件

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包含基底的 R 封裝和工具的完整分佈。 如需包含基底分佈的詳細資訊，請參閱文件會安裝在安裝期間於下列的預設位置︰
`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

為安裝的一部分 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，您必須同意 GNU 公用授權條款。 之後，您可以執行標準的 R 封裝，不需要進一步修改就如同在其他開放原始碼發佈是。

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 不會修改 R 執行階段以任何方式。 R 執行階段執行外部 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 處理，而且可以獨立執行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 不過，我們強烈建議您不要執行這些工具時 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 R 來避免資源爭用。

具有特定相關聯之 R 基底封裝發佈 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 可以在執行個體相關聯的資料夾中找到執行個體。 例如，如果預設執行個體上安裝 R 的服務，R 程式庫會位於 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`。

同樣地，預設執行個體相關聯的 R 工具將位於 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`,，

如需基底分佈的詳細資訊，請參閱 [Microsoft R open 安裝封裝](https://mran.revolutionanalytics.com/rro/installed/)

### 其他 R 封裝

除了基底的 R 分佈， [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包含一些專屬的 R 封裝，以及用來平行執行的 R 和程式庫支援在遠端的計算內容中執行的 R 的架構。 

-R 基底發佈加上增強的 R 功能和封裝-R 功能這個組合稱為 **Microsoft R**。如果您安裝 Microsoft R 伺服器 （獨立），您會取得完全相同的一組 SQL Server R 服務 （資料庫），但不同的資料夾中安裝的封裝。 

Microsoft R 包括 Intel 數學核心程式庫，它用於盡快數學程序的分佈。 例如，基本線性代數 (BLAS) 程式庫適用於許多與 R 本身也附加套件。 如需詳細資訊，請參閱下列文章︰

+ [Intel 數學核心如何加快 R](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [R 連結多執行緒的數學程式庫的效能優勢](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Microsoft 最重要的新增項目，其中包括 **RevoScaleR** 和 **RevoPemaR** 封裝。 這些是已寫入 C 或 c + + 中的主要是為了達到最佳效能的 R 封裝。

+ **RevoScaleR。** 包含各種不同的 Api 進行資料操作和分析。 Api 已經過最佳化，分析過大而無法納入記憶體，並執行計算分散在數個核心或處理器的資料集。

   RevoScaleR Api 也支援使用資料子集的更佳的延展性。 換句話說，大多數 RevoScaleR 函式可以操作區塊 （chunk） 的資料，以及使用更新彙總結果的演算法。 因此 R RevoScaleR 函式為基礎的解決方案可以使用非常大的資料集，而且不受限於本機記憶體。

  RevoScaleR 套件也支援。更快速移動資料和儲存用於分析的 XDF 檔案格式。 XDF 格式會使用單欄式儲存體、 可攜性，且可用來載入，然後操作從各種來源，包括文字、 SPSS、 或 ODBC 連接的資料。 在本教學課程提供如何使用 XDF 格式的範例︰ [資料科學深入探討](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)


+ **RevoPemaR。** PEMA 代表平行外部記憶體演算法。  **RevoPemaR** 套件提供 Api，可用來開發您自己的平行演算法。 如需詳細資訊，請參閱 [RevoPemaR 入門指南](https://msdn.microsoft.com/microsoft-r/rserver/rserver-pemar-getting-started)。

## 另請參閱
[架構概觀](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)

[在 SQL Server 支援 R 服務中的新元件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)

[安全性概觀](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)
