---
title: 掛接 S3 進行 HDFS 階層處理
titleSuffix: SQL Server big data clusters
description: 本文說明如何設定 HDFS 階層處理, 以將外部 S3 檔案系統掛接到 SQL Server 2019 big data cluster (預覽) 上的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 28c80d6076f07c8a4f1605149f4b5c730c8349a1
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419335"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>如何在大型資料叢集中掛接 S3 以進行 HDFS 分層

下列各節提供如何使用 S3 儲存體資料來源設定 HDFS 階層式範例。

## <a name="prerequisites"></a>先決條件

- [已部署 big data 叢集](deployment-guidance.md)
- [海量資料工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- 建立資料並將其上傳至 S3 bucket 
  - 將 CSV 或 Parquet 檔案上傳至您的 S3 bucket。 這是將掛接到 big data 叢集中 HDFS 的外部 HDFS 資料。

## <a name="access-keys"></a>存取金鑰

### <a name="set-environment-variable-for-access-key-credentials"></a>設定存取金鑰認證的環境變數

在可存取您 big data 叢集的用戶端電腦上開啟命令提示字元。 使用下列格式來設定環境變數。 請注意, 認證必須在逗號分隔清單中。 ' Set ' 命令是在 Windows 上使用。 如果您使用 Linux, 請改用 [匯出]。

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > 如需有關如何建立 S3 存取金鑰的詳細資訊, 請參閱[S3 存取金鑰](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)。

## <a id="mount"></a>掛接遠端 HDFS 儲存體

現在您已備妥具有存取金鑰的認證檔案, 您可以開始裝載。 下列步驟會將 S3 中的遠端 HDFS 儲存體掛接到 big data 叢集的本機 HDFS 儲存體。

1. 使用**kubectl**在您的 big data 叢集中尋找端點**控制器-svc-外部**服務的 IP 位址。 尋找 [**外部 IP**]。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 使用具有叢集使用者名稱和密碼的控制器端點的外部 IP 位址, 以**azdata**登入:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. 遵循上述指示設定環境變數 MOUNT_CREDENTIALS

1. 使用**azdata bdc 存放集區掛接建立**, 在 Azure 中掛接遠端 HDFS 儲存體。 執行下列命令之前, 請先取代預留位置值:

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > 掛接 create 命令是非同步。 此時, 沒有任何訊息指出掛接是否成功。 請參閱[狀態](#status)一節, 以檢查您的裝載狀態。

如果已成功掛接, 您應該能夠查詢 HDFS 資料, 並對其執行 Spark 作業。 它會出現在您的 big data 叢集的 HDFS 中, 並位於所`--mount-path`指定的位置。

## <a id="status"></a>取得裝載的狀態

若要列出海量資料叢集中所有裝載的狀態, 請使用下列命令:

```bash
azdata bdc storage-pool mount status
```

若要列出 HDFS 中特定路徑的掛接狀態, 請使用下列命令:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>重新整理掛接

下列範例會重新整理掛接。

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>刪除掛接

若要刪除掛接, 請使用**azdata bdc 存放集區掛接刪除**命令, 並在 HDFS 中指定掛接路徑:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)。
