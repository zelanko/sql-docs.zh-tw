---
title: 掛接 ADLS Gen2 進行 HDFS 階層處理
titleSuffix: How to mount ADLS Gen2
description: 這篇文章說明如何設定外部 Azure 資料湖儲存區檔案系統掛接到 HDFS，在 SQL Server 2019 巨量資料叢集 （預覽） 上的階層處理的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 504559fab3078b03ea3b8aea923035654f60ce47
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782137"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>如何針對 HDFS 層的巨量資料叢集掛接 ADLS Gen2

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

## <a name="credentials-for-mounting"></a>掛接的認證

## <a name="use-oauth-credentials-to-mount"></a>使用 OAuth 認證來掛接

若要使用 OAuth 認證，若要掛接，您必須遵循下列步驟：

1. 移至[Azure 入口網站](https://portal.azure.com)
1. 請移至 「 服務 」，在左側的導覽窗格中，和時鐘上 [Azure Active Directory]
1. 您可以使用 [應用程式註冊] 功能表中，建立 「 Web 應用程式並遵循精靈。 **請記住您在此處建立的名稱**。 您必須將這個名稱新增至您的 ADLS 帳戶，作為授權的使用者。
1. 一旦建立 web 應用程式時，請移至 [金鑰] 下 [設定] 應用程式。
1. 選取金鑰的持續時間，然後按一下 [儲存]。 **儲存產生的金鑰。**
1.  回到 [應用程式註冊] 頁面中，並按一下頂端的 [端點] 按鈕。 **請記下的 [權杖端點] URL**
1. 您現在應該有 for OAuth 記下的下列事項：

    - Web 應用程式的 「 應用程式識別碼 」 您先前建立在步驟 3
    - 您在步驟 5 中產生的金鑰
    - 步驟 6 中的權杖端點

### <a name="adding-the-service-principal-to-your-adls-account"></a>將服務主體新增至您的 ADLS 帳戶

1. 同樣地，請移至入口網站並且開啟您的 ADLS 帳戶，在左側功能表中選取存取控制 (IAM)。
1. 選取 [新增角色指派]，並搜尋您在步驟 3 中建立 （請注意，它不會顯示在清單中，但會找不到是否您搜尋完整名稱） 上方的名稱。
1. 現在加入 「 儲存體 Blob 資料參與者 （預覽） 」 角色。

等候 5-10 分鐘，再使用的認證進行裝載

### <a name="create-credential-file"></a>建立認證檔案

開啟命令提示字元可存取您的巨量資料叢集的用戶端電腦上。

建立名為本機檔案**filename.creds** ，其中包含您使用下列格式的 Azure Data Lake 儲存體 Gen2 帳戶認證：

   ```text
    fs.azure.account.auth.type=OAuth
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above]
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above]
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>使用存取金鑰來掛接

此外，您也可以掛上使用存取金鑰，您可以為您的 ADLS 帳戶，在 Azure 入口網站上取得。

 > [!TIP]
   > 如需有關如何尋找存取金鑰 (`<storage-account-access-key>`) 儲存體帳戶，請參閱[檢視及複製存取金鑰](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys)。

### <a name="create-credential-file"></a>建立認證檔案

1. 開啟命令提示字元可存取您的巨量資料叢集的用戶端電腦上。

1. 建立名為本機檔案**filename.creds** ，其中包含您使用下列格式的 Azure Data Lake 儲存體 Gen2 帳戶認證：

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> 掛接遠端 HDFS 儲存體

現在您已備妥的便捷鍵或使用 OAuth 的認證檔案，您可以開始掛接。 下列步驟會掛接到本機 HDFS 儲存體，您的巨量資料叢集的 Azure Data Lake 中遠端 HDFS 儲存。

1. 使用**kubectl**若要尋找 IP 位址端點**控制站 svc 外部**巨量資料叢集服務。 尋求**EXTERNAL-IP**。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 登入**mssqlctl**控制器端點的外部 IP 位址使用您的叢集使用者名稱和密碼：

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```

1. 掛接在 Azure 中使用遠端 HDFS 儲存體**mssqlctl 叢集存放集區掛接建立**。 將預留位置值，再執行下列命令：

   ```bash
   mssqlctl cluster storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > 掛接會建立命令是非同步的。 在此階段中，沒有任何訊息，指出連接是否成功。 請參閱[狀態](#status)一節，查看您掛接的狀態。

如果已成功掛接，您應能夠查詢 HDFS 資料，並對它執行 Spark 作業。 它會顯示在所指定的位置中的巨量資料叢集的 HDFS `--mount-path`。

## <a id="status"></a> 取得狀態的掛接

若要列出所有掛接在您的巨量資料叢集的狀態，請使用下列命令：

```bash
mssqlctl cluster storage-pool mount status
```

若要列出在 HDFS 中的特定路徑掛上的狀態，請使用下列命令：

```bash
mssqlctl cluster storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 刪除掛接

若要刪除掛接，請使用**mssqlctl 叢集儲存體集區掛接刪除**命令，並在 HDFS 中指定掛接路徑：

```bash
mssqlctl cluster storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
