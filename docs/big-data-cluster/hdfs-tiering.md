---
title: 設定 HDFS 的階層處理
titleSuffix: SQL Server big data clusters
description: 這篇文章說明如何設定外部 Azure 資料湖儲存區檔案系統掛接到 HDFS，在 SQL Server 2019 巨量資料叢集 （預覽） 上的階層處理的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2542c7c05b222517ae9f4a4c05152f21a5ba293b
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/02/2019
ms.locfileid: "58859640"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>設定 SQL Server 的巨量資料叢集上的階層處理的 HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 分層讓您能夠裝載外部，HDFS 中的 HDFS 相容檔案系統。 這篇文章說明如何設定 SQL Server 2019 巨量資料叢集 （預覽） 的階層處理的 HDFS。 此時，CTP 2.4 只支援連接到 Azure Data Lake 儲存體 Gen2，也就是本文的重點。

## <a name="hdfs-tiering-overview"></a>HDFS 分層概觀

與階層處理，應用程式可以順暢地存取各種不同的外部存放區中的資料就好像資料位於 HDFS。 掛接是中繼資料的作業，其中描述命名空間外部的檔案系統的中繼資料複製到 HDFS。 此中繼資料包括外部的目錄和檔案，以及它們的權限和 Acl 的相關資訊。 對應的資料時，只複製的視資料本身的存取。 從 SQL Server 的巨量資料叢集時，可以立即存取外部的檔案系統資料。 您可以執行 Spark 作業和 SQL 查詢此資料在相同的方式，您可以將它們執行儲存在 HDFS 在叢集上任何本機資料。

> [!NOTE]
> HDFS 的階層處理是 Microsoft 所開發的功能並較早版本的它已發行為 Apache Hadoop 3.1 散發的一部分。 如需詳細資訊，請參閱 < [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806)如需詳細資訊。

下列各節提供如何設定 HDFS 階層處理的 Azure Data Lake 儲存體 Gen2 資料來源的範例。

## <a name="prerequisites"></a>先決條件

- [已部署的巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a id="load"></a> 將資料載入 Azure Data Lake 儲存體

下一節會說明如何設定 Azure Data Lake 儲存體 Gen2 測試 HDFS 的階層處理。 如果您已經有儲存在 Azure Data Lake 儲存體中的資料，您可以略過此區段可使用您自己的資料。

1. [建立儲存體帳戶與 Data Lake 儲存體 Gen2 功能](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)。

1. [建立 blob 容器](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal)這個外部資料的儲存體帳戶中。

1. 將 CSV 或 Parquet 檔案上傳至容器。 這是將會掛接到 HDFS 中的巨量資料叢集外部 HDFS 資料。

## <a id="mount"></a> 掛接遠端 HDFS 儲存體

下列步驟會掛接到本機 HDFS 儲存體，您的巨量資料叢集的 Azure Data Lake 中遠端 HDFS 儲存。

1. 開啟命令提示字元可存取您的巨量資料叢集的用戶端電腦上。

1. 建立名為本機檔案**files.creds** ，其中包含您使用下列格式的 Azure Data Lake 儲存體 Gen2 帳戶認證：

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

   > [!TIP]
   > 如需有關如何尋找存取金鑰 (`<storage-account-access-key>`) 儲存體帳戶，請參閱[檢視及複製存取金鑰](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys)。

1. 使用**kubectl**若要尋找 IP 位址**端點服務 proxy**巨量資料叢集服務。 尋求**EXTERNAL-IP**。

   ```bash
   kubectl get svc endpoint-service-proxy -n <your-cluster-name>
   ```

1. 登入**mssqlctl**服務 proxy 端點使用您的叢集使用者名稱和密碼：

   ```bash
   mssqlctl login -e https://<IP-of-endpoint-service-proxy>:30777/ -u <username> -p <password>
   ```

1. 掛接在 Azure 中使用遠端 HDFS 儲存體**mssqlctl 儲存體掛接建立**。 將預留位置值，再執行下列命令：

   ```bash
   mssqlctl storage mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > 掛接會建立命令是非同步的。 在此階段中，沒有任何訊息，指出連接是否成功。 請參閱[狀態](#status)一節，查看您掛接的狀態。

如果已成功掛接，您應能夠查詢 HDFS 資料，並對它執行 Spark 作業。 它會顯示在所指定的位置中的巨量資料叢集的 HDFS `--local-path`。

## <a id="status"></a> 取得狀態的掛接

若要列出所有掛接在您的巨量資料叢集的狀態，請使用下列命令：

```bash
mssqlctl storage mount status
```

若要列出在 HDFS 中的特定路徑掛上的狀態，請使用下列命令：

```bash
mssqlctl storage mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 刪除掛接

若要刪除掛接，請使用**mssqlctl 儲存體掛接刪除**命令，並在 HDFS 中指定掛接路徑：

```bash
mssqlctl storage mount delete --mount-path <mount-path-in-hdfs>
```

## <a id="issues"></a> 已知的問題和限制

使用 HDFS 層的 SQL Server 的巨量資料叢集時，下列清單提供已知的問題和目前限制：

- 如果外部掛接的目錄的大小大於叢集容量，掛接將會失敗。

- 如果掛接陷入`CREATING`狀態很長的時間，最有可能失敗。 在此情況下，取消命令，並在必要時刪除掛接。 確認您的參數和認證正確無誤後再重試。

- 無法建立掛接上現有的目錄。

- 無法建立掛接內現有的掛接。

- 如果不存在任何掛接點的上階，它們將會建立具有權限預設為 r-xr-xr-x (555)。

- 掛接建立可能需要一些時間，視所掛接的檔案大小與數量而定。 在此過程中下掛接, 的檔案不是對使用者顯示。 建立掛接時，會所有的檔案新增至暫存路徑，預設為`/_temporary/_mounts/<mount-location>`。

- 掛上建立命令是非同步的。 命令執行之後，可以檢查掛接狀態，以了解掛接的狀態。

- 引數建立時掛接，已用於 **-本機路徑**是本質上掛接的唯一識別碼。 在後續命令中，必須使用相同的字串 （包括"/"結尾，如果有的話）。

- 掛接為唯讀。 您無法建立任何目錄或下掛接的檔案。

- 我們不建議掛接目錄和檔案，可以變更。 建立掛接之後，任何變更或更新至遠端位置將不會反映在 HDFS 中掛接。 如果在遠端位置執行發生變更，您可以選擇刪除並重新建立掛接，以反映更新的狀態。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
