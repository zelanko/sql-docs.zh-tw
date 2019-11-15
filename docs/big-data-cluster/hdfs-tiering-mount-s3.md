---
title: 掛接 S3 進行 HDFS 階層處理
titleSuffix: SQL Server big data clusters
description: 本文說明如何設定 HDFS 階層處理，以將外部 S3 檔案系統掛接到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]上的 HDFS 中。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 653f9a48c03df18fc0591f7bd8060d951567c779
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652300"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>如何在巨量資料叢集中掛接 S3 以進行 HDFS 階層處理

下列各節提供如何使用 S3 儲存體資料來源設定 HDFS 階層處理的範例。

## <a name="prerequisites"></a>Prerequisites

- [部署巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- 建立資料並上傳到 S3 貯體 
  - 將 CSV 或 Parquet 檔案上傳到您的 S3 貯體。 這是將掛接到巨量資料叢集中 HDFS 的外部 HDFS 資料。

## <a name="access-keys"></a>存取金鑰

### <a name="set-environment-variable-for-access-key-credentials"></a>設定存取金鑰認證的環境變數

在可存取您巨量資料叢集的用戶端電腦上開啟命令提示字元。 使用下列格式來設定環境變數。 請注意，認證必須位於逗號分隔清單中。 'set' 命令是在 Windows 上使用的。 如果您使用 Linux，請改為使用 'export'。

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > 如需有關如何建立 S3 存取金鑰的詳細資訊，請參閱[S3 存取金鑰](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)。

## <a id="mount"></a> 掛接遠端 HDFS 儲存體

現在您已備妥具有存取金鑰的認證檔案，您可以開始裝載。 下列步驟會將 S3 中的遠端 HDFS 儲存體掛接到您巨量資料叢集的本機 HDFS 儲存體。

1. 使用 **kubectl** 在您的巨量資料叢集中尋找端點 **controller-svc-external** 服務的 IP 位址。 尋找 **External-IP**。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 使用您的使用者名稱與密碼，利用 **azdata** 透過控制器端點的外部 IP 位址登入：

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. 依照上面的指示設定環境變數 MOUNT_CREDENTIALS

1. 使用 **azdata bdc hdfs mount create** 在 Azure 中掛接遠端 HDFS 儲存體。 執行下列命令之前，請先取代預留位置值：

   ```bash
   azdata bdc hdfs mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > mount create 是非同步命令。 此時，沒有任何訊息指出掛接是否成功。 請參閱[狀態](#status)一節以檢查您的掛接狀態。

如果已成功掛接，您應該能夠查詢 HDFS 資料，並對其執行 Spark 作業。 掛接會出現在您巨量資料叢集的 HDFS 中，位於 `--mount-path` 所指定的位置。

## <a id="status"></a> 取得掛接的狀態

若要列出巨量資料叢集中所有掛接的狀態，請使用下列命令：

```bash
azdata bdc hdfs mount status
```

若要列出 HDFS 中特定路徑的掛接狀態，請使用下列命令：

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>重新整理掛接

下列範例會重新整理掛接。

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 刪除掛接

若要刪除掛接，請使用 **azdata bdc hdfs mount delete** 命令，並在 HDFS 中指定掛接路徑：

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
