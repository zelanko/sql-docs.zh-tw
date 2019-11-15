---
title: 設定 HDFS 階層處理
titleSuffix: SQL Server big data clusters
description: 本文說明如何設定 HDFS 階層處理，以便能將外部 Azure Data Lake Storage 檔案系統掛接到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的 HDFS 上。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 673b3eed760af4b36c494e2dd45cdfc8ed8e8dc8
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706048"
---
# <a name="configure-hdfs-tiering-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上設定 HDFS 階層處理

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 階層處理提供在 HDFS 中掛接外部、HDFS 相容檔案系統的功能。 本文說明如何為 SQL Server 巨量資料叢集設定 HDFS 階層處理。 目前，我們支援連線至 Azure Data Lake Storage Gen2 和 Amazon S3。 

## <a name="hdfs-tiering-overview"></a>HDFS 階層處理概觀

應用程式可以透過階層處理順暢存取各種外部存放區中的資料，如同資料位於本機 HDFS 一樣。 掛接是中繼資料作業，其中描述外部檔案系統上命名空間的中繼資料會複製到本機 HDFS。 此中繼資料包含外部目錄和檔案的相關資訊，以及其權限和 ACL。 對應的資料只會隨選複製，而資料本身則是透過查詢等項目來存取。 您現在可以從 SQL Server 巨量資料叢集存取外部檔案系統資料。 您可以對此資料執行 Spark 作業和 SQL 查詢，方式與在叢集上儲存於 HDFS 的任何本機資料上執行它們一樣。

### <a name="caching"></a>Caching
根據預設，現在會保留 1% 的總 HDFS 儲存體，來快取已掛接的資料。 快取是跨掛接的全域設定。

> [!NOTE]
> HDFS 階層處理是由 Microsoft 開發的功能，其舊版已發行為 Apache Hadoop 3.1 發行版本的一部分。 如需詳細資訊，請參閱 [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806) 以取得詳細資料。

下列各節提供如何使用 Azure Data Lake Storage Gen2 儲存體資料來源來設定 HDFS 階層處理的範例。

## <a name="refresh"></a>Refresh

HDFS 階層處理支援重新整理。 針對遠端資料的最新快照集重新整理現有掛接。

## <a name="prerequisites"></a>Prerequisites

- [部署巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>掛接說明

我們支援連線至 Azure Data Lake Storage Gen2 和 Amazon S3。 如需針對這些儲存體類型進行掛接的說明，請參閱下列文章：

- [如何在巨量資料叢集中掛接 ADLS Gen2 以進行 HDFS 階層處理](hdfs-tiering-mount-adlsgen2.md)
- [如何在巨量資料叢集中掛接 S3 以進行 HDFS 階層處理](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> 已知問題和限制

下列清單提供在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]中使用 HDFS 階層處理時的已知問題和目前限制：

- 如果掛接長時間停滯在 `CREATING` 狀態中，則可能已失敗。 在此情況下，請取消命令並視需要刪除掛接。 請先確認您的參數和認證是否正確再重試。

- 您無法在現有的目錄上建立掛接。

- 您無法在現有的掛接內建立掛接。

- 如果掛接點沒有任何上階，則會使用預設為 r-xr-xr-x (555) 的權限來建立。

- 建立掛接可能需要一些時間，視掛接的檔案數目和大小而定。 在此程序中，使用者看不到掛接下方的檔案。 建立掛接時，所有檔案都會新增至暫存路徑，預設為 `/_temporary/_mounts/<mount-location>`。

- 掛接建立命令是非同步的。 在執行命令之後，您可以檢查掛接狀態以了解掛接的目前狀態。

- 在建立掛接時，用於 **--mount-path** 的引數，基本上就是掛接的唯一識別碼。 在後續命令中也必須使用相同的字串 (若有，請在結尾處包含 "/")。

- 掛接是唯讀的。 您無法在掛接下方建立任何目錄或檔案。

- 我們不建議您掛接可變更的目錄和檔案。 建立掛接之後，任何對遠端位置的變更或更新，將不會反映在 HDFS 的掛接中。 如果遠端位置發生變更，您可以選擇刪除並重新建立掛接以反映更新的狀態。

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
