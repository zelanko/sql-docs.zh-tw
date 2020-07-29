---
title: 掛接 ADLS Gen2 進行 HDFS 階層處理
titleSuffix: How to mount ADLS Gen2
description: 本文說明如何設定 HDFS 階層處理，以將外部 Azure Data Lake Storage 檔案系統掛接到 SQL Server 2019 巨量資料叢集上的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/29/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b0206ca193e6c03624c0d40d0c66e7474b00a7a0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730651"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>如何在巨量資料叢集中掛接 ADLS Gen2 以進行 HDFS 階層處理

下列各節提供如何使用 Azure Data Lake Storage Gen2 儲存體資料來源來設定 HDFS 階層處理的範例。

## <a name="prerequisites"></a>Prerequisites

- [部署巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="load-data-into-azure-data-lake-storage"></a><a id="load"></a> 將資料載入 Azure Data Lake Storage

下節描述如何設定 Azure Data Lake Storage Gen2 來測試 HDFS 階層處理。 如果您已經有資料儲存在 Azure Data Lake Storage 中，則可以略過本節並使用您自己的資料。

1. [建立具有 Data Lake Storage Gen2 功能的儲存體帳戶。](/azure/storage/blobs/data-lake-storage-quickstart-create-account)

1. 在此儲存體帳戶中，為資料[建立檔案系統](/azure/storage/blobs/data-lake-storage-explorer)。

1. 將 CSV 或 Parquet 檔案上傳至容器。 這是將會掛接到巨量資料叢集中 HDFS 的外部 HDFS 資料。

## <a name="credentials-for-mounting"></a>用於掛接的認證

### <a name="use-oauth-credentials-to-mount"></a>使用 OAuth 認證來掛接

若要使用 OAuth 認證來掛接，您必須遵循下列步驟：

1. 前往 [Azure 入口網站](https://portal.azure.com)
1. 瀏覽至 [Azure Active Directory]。 左側導覽列上應會顯示此服務。
1. 從右側導覽列中選取 [應用程式註冊]，然後建立新的註冊
1. 建立 Web 應用程式並遵循精靈。 **請記下您此處建立之用程式的稱**。 您必須將此名稱新增至您的 ADLS 帳戶作為授權使用者。 另請記下您選取此應用時，概觀中顯示的應用程式用戶端識別碼。
1. 建立 Web 應用程式之後，請移至 [憑證及密碼] 並建立**新的用戶端密碼**，然後選取金鑰期間。 **新增**此密碼。
1. 返回 [應用程式註冊] 頁面，然後按一下頂端的 [端點]。 **記下 OAuth 權杖端點 (v2)** URL
1. 您現在應該已記下 OAuth 的下列項目：

    - Web 應用程式的「應用程式用戶端識別碼」
    - 用戶端密碼
    - 權杖端點

### <a name="adding-the-service-principal-to-your-adls-account"></a>將服務主體新增至您的 ADLS 帳戶

1. 再次前往入口網站，並瀏覽至您的 ADLS 儲存體帳戶檔案系統，然後選取左側功能表中的 [存取控制 (IAM)]。
1. 選取 [新增角色指派] 
1. 選取角色 [儲存體 Blob 資料參與者]
1. 搜尋您在上述步驟中建立的名稱 (請注意，該名稱不會顯示在清單中，但若是搜尋完整名稱就可找到)。
1. 儲存該角色。

請等候 5-10 分鐘，再使用認證來進行掛接

### <a name="set-environment-variable-for-oauth-credentials"></a>設定 OAuth 認證的環境變數

在可存取您巨量資料叢集的用戶端電腦上開啟命令提示字元。 使用下列格式設定環境變數。認證必須位於逗號分隔的清單中。 'set' 命令是在 Windows 上使用的。 如果您使用 Linux，請改為使用 'export'。

**請注意**，提供認證時，請務必移除逗號 "," 之間的所有分行符號或空格。 下列格式比較容易閱讀。

```console
   set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
   fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
   fs.azure.account.oauth2.client.endpoint=[token endpoint],
   fs.azure.account.oauth2.client.id=[Application client ID],
   fs.azure.account.oauth2.client.secret=[client secret]
```

## <a name="use-access-keys-to-mount"></a>使用存取金鑰來掛接

您也可以使用可在 Azure 入口網站上為您 ADLS 帳戶取得的存取金鑰來進行掛接。

 > [!TIP]
   > 如需如何尋找儲存體帳戶存取金鑰 (`<storage-account-access-key>`) 的詳細資訊，請參閱[檢視帳戶金鑰和連接字串](/azure/storage/common/storage-account-keys-manage#view-access-keys-and-connection-string)。

### <a name="set-environment-variable-for-access-key-credentials"></a>設定存取金鑰認證的環境變數

1. 在可存取您巨量資料叢集的用戶端電腦上開啟命令提示字元。

1. 在可存取您巨量資料叢集的用戶端電腦上開啟命令提示字元。 使用下列格式來設定環境變數。 認證必須位於逗號分隔的清單中。 'set' 命令是在 Windows 上使用的。 如果您使用 Linux，請改為使用 'export'。

**請注意**，提供認證時，請務必移除逗號 "," 之間的所有分行符號或空格。 下列格式比較容易閱讀。

```console
set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
```

## <a name="mount-the-remote-hdfs-storage"></a><a id="mount"></a> 掛接遠端 HDFS 儲存體

現在您已設定存取金鑰的 MOUNT_CREDENTIALS 環境變數或使用 OAuth，您即可以開始掛接。 下列步驟會將 Azure Data Lake 中的遠端 HDFS 儲存體，掛接到您巨量資料叢集的本機 HDFS 儲存體。

1. 使用 **kubectl** 在您的巨量資料叢集中尋找端點 **controller-svc-external** 服務的 IP 位址。 尋找 **External-IP**。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 使用您的使用者名稱與密碼，利用 **azdata** 透過控制器端點的外部 IP 位址登入：

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080
   ```
1. 設定環境變數 MOUNT_CREDENTIALS (向上捲動以取得指示)

1. 使用 **azdata bdc hdfs mount create** 在 Azure 中掛接遠端 HDFS 儲存體。 執行下列命令之前，請先取代預留位置值：

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > mount create 是非同步命令。 此時，沒有任何訊息指出掛接是否成功。 請參閱[狀態](#status)一節以檢查您的掛接狀態。

如果已成功掛接，您應該能夠查詢 HDFS 資料，並對其執行 Spark 作業。 掛接會出現在您巨量資料叢集的 HDFS 中，位於 `--mount-path` 所指定的位置。

## <a name="get-the-status-of-mounts"></a><a id="status"></a> 取得掛接的狀態

若要列出巨量資料叢集中所有掛接的狀態，請使用下列命令：

```bash
azdata bdc hdfs mount status
```

若要列出 HDFS 中特定路徑的掛接狀態，請使用下列命令：

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>重新整理掛接

下列範例會重新整理掛接。 此重新整理也會清除掛接快取。

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a name="delete-the-mount"></a><a id="delete"></a> 刪除掛接

若要刪除掛接，請使用 **azdata bdc hdfs mount delete** 命令，並在 HDFS 中指定掛接路徑：

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
