---
title: 設定 HDFS 的階層處理
titleSuffix: SQL Server big data clusters
description: 這篇文章說明如何設定外部 Azure 資料湖儲存區檔案系統掛接到 HDFS，在 SQL Server 2019 巨量資料叢集 （預覽） 上的階層處理的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a36bd28efd128a76246297995d712b417d7f230d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782107"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>設定 SQL Server 的巨量資料叢集上的階層處理的 HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 分層讓您能夠裝載外部，HDFS 中的 HDFS 相容檔案系統。 這篇文章說明如何設定 SQL Server 2019 巨量資料叢集 （預覽） 的階層處理的 HDFS。 在此階段中，我們支援連線到 Azure Data Lake 儲存體 Gen2 和 Amazon S3。 

## <a name="hdfs-tiering-overview"></a>HDFS 分層概觀

與階層處理，應用程式可以順暢地存取各種不同的外部存放區中的資料就好像資料位於本機 HDFS。 掛接是中繼資料的作業，其中描述命名空間外部的檔案系統的中繼資料複製到您本機 HDFS。 此中繼資料包括外部的目錄和檔案，以及它們的權限和 Acl 的相關資訊。 相對應的資料時，只複製的隨，透過例如的查詢存取資料本身。 從 SQL Server 的巨量資料叢集時，可以立即存取外部的檔案系統資料。 您可以執行 Spark 作業和 SQL 查詢此資料在相同的方式，您可以將它們執行儲存在 HDFS 在叢集上任何本機資料。

### <a name="caching"></a>Caching
現在，根據預設，1%的總 HDFS 儲存體將保留供快取的已掛接的資料。 快取是透過掛接的全域設定。

> [!NOTE]
> HDFS 的階層處理是 Microsoft 所開發的功能並較早版本的它已發行為 Apache Hadoop 3.1 散發的一部分。 如需詳細資訊，請參閱 < [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806)如需詳細資訊。

下列各節提供如何設定 HDFS 階層處理的 Azure Data Lake 儲存體 Gen2 資料來源的範例。

## <a name="prerequisites"></a>先決條件

- [已部署的巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a name="mounting-instructions"></a>裝載指示

我們支援連線到 Azure Data Lake 儲存體 Gen2 和 Amazon S3。 如何針對這些儲存體類型掛接上的指示，請參閱下列文章：

- [如何針對 HDFS 層的巨量資料叢集掛接 ADLS Gen2](hdfs-tiering-mount-adlsgen2.md)
- [如何掛接 S3 層的巨量資料叢集的 HDFS 的](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> 已知的問題和限制

使用 HDFS 層的 SQL Server 的巨量資料叢集時，下列清單提供已知的問題和目前限制：

- 如果掛接陷入`CREATING`狀態很長的時間，最有可能失敗。 在此情況下，取消命令，並在必要時刪除掛接。 確認您的參數和認證正確無誤後再重試。

- 無法建立掛接上現有的目錄。

- 無法建立掛接內現有的掛接。

- 如果不存在任何掛接點的上階，它們將會建立具有權限預設為 r-xr-xr-x (555)。

- 掛接建立可能需要一些時間，視所掛接的檔案大小與數量而定。 在此過程中下掛接, 的檔案不是對使用者顯示。 建立掛接時，會所有的檔案新增至暫存路徑，預設為`/_temporary/_mounts/<mount-location>`。

- 掛上建立命令是非同步的。 命令執行之後，可以檢查掛接狀態，以了解掛接的狀態。

- 引數建立時掛接，已用於 **-掛接路徑**是本質上掛接的唯一識別碼。 在後續命令中，必須使用相同的字串 （包括"/"結尾，如果有的話）。

- 掛接為唯讀。 您無法建立任何目錄或下掛接的檔案。

- 我們不建議掛接目錄和檔案，可以變更。 建立掛接之後，任何變更或更新至遠端位置將不會反映在 HDFS 中掛接。 如果在遠端位置執行發生變更，您可以選擇刪除並重新建立掛接，以反映更新的狀態。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
