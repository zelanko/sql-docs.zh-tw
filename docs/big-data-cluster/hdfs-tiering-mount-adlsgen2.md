---
title: 掛接 ADLS Gen2 進行 HDFS 階層處理
titleSuffix: How to mount ADLS Gen2
description: 本文說明如何設定 HDFS 階層處理，以將外部 Azure Data Lake Storage 檔案系統掛接到 SQL Server 2019 巨量資料叢集 (預覽) 上的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 83922206503b690a7b49c27d4686333bf7b966a1
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742727"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>如何在巨量資料叢集中掛接 ADLS Gen2 以進行 HDFS 階層處理

下列各節提供如何使用 Azure Data Lake Storage Gen2 儲存體資料來源設定 HDFS 階層處理的範例。

## <a name="prerequisites"></a>必要條件

- [部署巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a> 將資料載入 Azure Data Lake Storage

下節描述如何設定 Azure Data Lake Storage Gen2 來測試 HDFS 階層處理。 如果您已經有資料儲存在 Azure Data Lake Storage 中，則可以略過本節並使用您自己的資料。

1. [建立具有 Data Lake Storage Gen2 功能的儲存體帳戶。](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)

1. 在此儲存體帳戶中為您的外部資料[建立 Blob 容器](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal)。

1. 將 CSV 或 Parquet 檔案上傳至容器。 這是將會掛接到巨量資料叢集中 HDFS 的外部 HDFS 資料。

## <a name="credentials-for-mounting"></a>用於掛接的認證

## <a name="use-oauth-credentials-to-mount"></a>使用 OAuth 認證來掛接

若要使用 OAuth 認證來掛接，您必須遵循下列步驟：

1. 前往 [Azure 入口網站](https://portal.azure.com)
1. 前往左側瀏覽窗格中的 [服務]，然後按一下 [Azure Active Directory]
1. 使用功能表中的 [應用程式註冊]，建立「Web 應用程式」並遵循精靈。 **請記住您在此處建立的名稱**。 您必須將此名稱新增至您的 ADLS 帳戶作為授權使用者。
1. 建立 Web 應用程式之後，請前往應用程式 [設定] 下方的 [金鑰]。
1. 選取金鑰持續時間，然後按一下 [儲存]。 **儲存產生的金鑰。**
1.  回到 [應用程式註冊] 頁面，然後按一下頂端的 [端點] 按鈕。 **記下「權杖端點」URL**
1. 您現在應該已記下 OAuth 的下列項目：

    - 您在步驟 3 中所建立 Web 應用程式的「應用程式識別碼」
    - 您剛剛在步驟 5 中產生的金鑰
    - 步驟 6 的權杖端點

### <a name="adding-the-service-principal-to-your-adls-account"></a>將服務主體新增至您的 ADLS 帳戶

1. 再次前往入口網站並開啟您的 ADLS 帳戶，然後選取左側功能表中的 [存取控制 (IAM)]。
1. 選取 [新增角色指派] 並搜尋您在上述步驟 3 中建立的名稱 (請注意，該名稱不會顯示在清單中，但在您搜尋完整名稱時可以找到)。
1. 現在新增「儲存體 Blob 資料參與者 (預覽)」角色。

請等候 5-10 分鐘，再使用認證來進行掛接

### <a name="set-environment-variable-for-oauth-credentials"></a>設定 OAuth 認證的環境變數

在可存取您巨量資料叢集的用戶端電腦上開啟命令提示字元。 使用下列格式來設定環境變數：請注意，認證必須位於逗號分隔清單中。 'set' 命令是在 Windows 上使用的。 如果您使用 Linux，請改為使用 'export'。

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>使用存取金鑰來掛接

您也可以使用可在 Azure 入口網站上為您 ADLS 帳戶取得的存取金鑰來進行掛接。

 > [!TIP]
   > 如需如何尋找儲存體帳戶存取金鑰 (`<storage-account-access-key>`) 的詳細資訊，請參閱[檢視帳戶金鑰和連接字串](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string)。

### <a name="set-environment-variable-for-access-key-credentials"></a>設定存取金鑰認證的環境變數

1. 在可存取您巨量資料叢集的用戶端電腦上開啟命令提示字元。

1. 在可存取您巨量資料叢集的用戶端電腦上開啟命令提示字元。 使用下列格式來設定環境變數。 請注意，認證必須位於逗號分隔清單中。 'set' 命令是在 Windows 上使用的。 如果您使用 Linux，請改為使用 'export'。

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> 掛接遠端 HDFS 儲存體

現在您已設定存取金鑰的 MOUNT_CREDENTIALS 環境變數或使用 OAuth，您即可以開始掛接。 下列步驟會將 Azure Data Lake 中的遠端 HDFS 儲存體，掛接到您巨量資料叢集的本機 HDFS 儲存體。

1. 使用 **kubectl** 在您的巨量資料叢集中尋找端點 **controller-svc-external** 服務的 IP 位址。 尋找 **External-IP**。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 使用您的使用者名稱與密碼，利用 **azdata** 透過控制器端點的外部 IP 位址登入：

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. 設定環境變數 MOUNT_CREDENTIALS (向上捲動以取得指示)

1. 使用**azdata bdc HDFS 掛接 create**, 在 Azure 中掛接遠端 HDFS 儲存體。 執行下列命令之前，請先取代預留位置值：

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
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

若要刪除掛接, 請使用**azdata bdc hdfs mount delete**命令, 並在 hdfs 中指定掛接路徑:

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>後續步驟

如需 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 [SQL Server 2019 巨量資料叢集是什麼](big-data-cluster-overview.md)。
