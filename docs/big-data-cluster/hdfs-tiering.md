---
title: 設定 HDFS 分層
titleSuffix: SQL Server big data clusters
description: 本文說明如何設定 HDFS 階層處理, 以將外部 Azure Data Lake Storage 檔案系統掛接到 SQL Server 2019 big Data cluster (預覽) 上的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17eedf9f0797a0adb5eda6ca8ee090fc762e1491
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419383"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>在 SQL Server big data 叢集上設定 HDFS 分層

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 分層提供在 HDFS 中掛接外部、HDFS 相容檔案系統的功能。 本文說明如何為 SQL Server 2019 big data 叢集 (預覽) 設定 HDFS 分層。 目前, 我們支援連接到 Azure Data Lake Storage Gen2 和 Amazon S3。 

## <a name="hdfs-tiering-overview"></a>HDFS 階層處理總覽

透過分層, 應用程式可以順暢地存取各種外部存放區中的資料, 就像資料位於本機 HDFS 一樣。 裝載是中繼資料作業, 其中描述外部檔案系統上之命名空間的中繼資料會複製到您的本機 HDFS。 此中繼資料包含外部目錄和檔案的相關資訊, 以及其許可權和 Acl。 對應的資料只會隨選複製, 而資料本身則是透過來存取, 例如查詢。 現在可以從 SQL Server big data 叢集存取外部檔案系統資料。 您可以對此資料執行 Spark 作業和 SQL 查詢, 其方式與在叢集上儲存于 HDFS 的任何本機資料上執行相同。

### <a name="caching"></a>Caching
今天, 根據預設, 會保留總 HDFS 儲存體的 1% 來快取已掛接的資料。 快取是跨裝載的全域設定。

> [!NOTE]
> HDFS 階層處理是由 Microsoft 開發的功能, 而舊版的階層已發行為 Apache Hadoop 3.1 散發套件的一部分。 如需詳細資訊, [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806)請參閱。

下列各節提供如何使用 Azure Data Lake Storage Gen2 資料來源設定 HDFS 階層式範例。

## <a name="refresh"></a>重新整理

HDFS 分層支援重新整理。 重新整理現有的掛接, 以取得遠端資料的最新快照集。

## <a name="prerequisites"></a>先決條件

- [已部署 big data 叢集](deployment-guidance.md)
- [海量資料工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>裝載指示

我們支援連接到 Azure Data Lake Storage Gen2 和 Amazon S3。 如需如何針對這些儲存體類型進行掛接的指示, 請參閱下列文章:

- [如何在大型資料叢集中掛接 HDFS 階層式 ADLS Gen2](hdfs-tiering-mount-adlsgen2.md)
- [如何在大型資料叢集中掛接 S3 以進行 HDFS 分層](hdfs-tiering-mount-s3.md)

## <a id="issues"></a>已知問題和限制

下列清單提供在 SQL Server big data 叢集中使用 HDFS 分層時的已知問題和目前的限制:

- 如果掛接長時間停滯在某個`CREATING`狀態中, 很可能會失敗。 在此情況下, 請取消命令, 並視需要刪除掛接。 請先確認您的參數和認證是否正確, 再重試。

- 無法在現有的目錄上建立裝載。

- 無法在現有的裝載內建立裝載。

- 如果掛接點的任何祖系不存在, 則會使用預設為 xr-xr-x (555) 的許可權來建立它們。

- 視裝載的檔案數目和大小而定, 掛接建立可能需要一些時間。 在此過程中, 使用者看不到掛接下的檔案。 建立掛接時, 會將所有檔案新增至暫存路徑, 預設為`/_temporary/_mounts/<mount-location>`。

- 掛接建立命令是非同步。 執行命令之後, 您可以檢查掛接狀態以瞭解掛接的狀態。

- 建立掛接時, 用於 **--掛接路徑**的引數基本上就是掛接的唯一識別碼。 在後續的命令中, 必須使用相同的字串 (如果有的話, 請在結尾包含 "/")。

- 裝載是唯讀的。 您無法在掛接下建立任何目錄或檔案。

- 我們不建議您裝載可變更的目錄和檔案。 建立掛接之後, 對遠端位置的任何變更或更新將不會反映在 HDFS 的掛接中。 如果在遠端位置發生變更, 您可以選擇刪除並重新建立掛接, 以反映更新的狀態。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)。
