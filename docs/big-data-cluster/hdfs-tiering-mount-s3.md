---
title: 掛接 S3 進行 HDFS 階層處理
titleSuffix: SQL Server big data clusters
description: 這篇文章說明如何設定 HDFS 上的 SQL Server 2019 巨量資料叢集 （預覽） 掛接到 HDFS 的外部 S3 檔案系統的階層處理。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 04/15/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 79c09d5bcff26c9f5867e5b0fb38bd019b681b5c
ms.sourcegitcommit: 89abd4cd4323ae5ee284571cd69a9fe07d869664
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "64330609"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>如何掛接 S3 層的巨量資料叢集的 HDFS 的

下列各節提供如何設定 HDFS 階層處理的 S3 儲存體資料來源的範例。

## <a name="prerequisites"></a>必要條件

- [已部署的巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**
- 建立並上傳資料至 S3 貯體 
  - 上傳 CSV 或 Parquet 檔案到您的 S3 貯體。 這是將會掛接到 HDFS 中的巨量資料叢集外部 HDFS 資料。

## <a name="access-keys"></a>存取金鑰

1. 開啟命令提示字元可存取您的巨量資料叢集的用戶端電腦上。

1. 建立名為本機檔案**filename.creds** ，其中包含您使用下列格式的 S3 帳戶認證：

   ```text
    fs.s3a.access.key=<Access Key ID of the key>
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > 如需有關如何建立 S3 存取金鑰的詳細資訊，請參閱 < [S3 便捷鍵](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)。

## <a id="mount"></a> 掛接遠端 HDFS 儲存體

既然您已備妥的認證檔案，以存取金鑰，您可以開始掛接。 下列步驟可裝載遠端 HDFS 中的儲存體 S3 到您的巨量資料叢集的本機 HDFS 儲存體。

1. 使用**kubectl**若要尋找 IP 位址**mgmtproxy svc 外部**巨量資料叢集服務。 尋求**EXTERNAL-IP**。

   ```bash
   kubectl get svc mgmtproxy-svc-external -n <your-cluster-name>
   ```

1. 登入**mssqlctl**管理 proxy 端點的外部 IP 位址使用您的叢集使用者名稱和密碼：

   ```bash
   mssqlctl login -e https://<IP-of-mgmtproxy-svc-external>:30777/ -u <username> -p <password>
   ```

1. 掛接在 Azure 中使用遠端 HDFS 儲存體**mssqlctl 儲存體掛接建立**。 將預留位置值，再執行下列命令：

   ```bash
   mssqlctl storage mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name> --credential-file <path-to-s3-credentials>/file.creds
   ```

   > [!NOTE]
   > 掛接會建立命令是非同步的。 在此階段中，沒有任何訊息，指出連接是否成功。 請參閱[狀態](#status)一節，查看您掛接的狀態。

如果已成功掛接，您應能夠查詢 HDFS 資料，並對它執行 Spark 作業。 它會顯示在所指定的位置中的巨量資料叢集的 HDFS `--mount-path`。

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

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
