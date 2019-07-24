---
title: 掛接 ADLS Gen2 進行 HDFS 階層處理
titleSuffix: How to mount ADLS Gen2
description: 本文說明如何設定 HDFS 階層處理, 以將外部 Azure Data Lake Storage 檔案系統掛接到 SQL Server 2019 big Data cluster (預覽) 上的 HDFS。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7d8a6dd53452700853dca9774ed0196ed7546fe
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419353"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>如何在大型資料叢集中掛接 HDFS 階層式 ADLS Gen2

下列各節提供如何使用 Azure Data Lake Storage Gen2 資料來源設定 HDFS 階層式範例。

## <a name="prerequisites"></a>必要條件

- [已部署 big data 叢集](deployment-guidance.md)
- [海量資料工具](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a>將資料載入 Azure Data Lake Storage

下一節說明如何設定 Azure Data Lake Storage Gen2 來測試 HDFS 分層。 如果您已經有儲存在 Azure Data Lake Storage 中的資料, 則可以略過本節以使用您自己的資料。

1. [建立具有 Data Lake Storage Gen2 功能的儲存體帳戶](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)。

1. 針對您的外部資料, 在此儲存體帳戶中[建立 blob 容器](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal)。

1. 將 CSV 或 Parquet 檔案上傳至容器。 這是將掛接到 big data 叢集中 HDFS 的外部 HDFS 資料。

## <a name="credentials-for-mounting"></a>裝載的認證

## <a name="use-oauth-credentials-to-mount"></a>使用 OAuth 認證來掛接

若要使用 OAuth 認證來掛接, 您必須遵循下列步驟:

1. 前往[Azure 入口網站](https://portal.azure.com)
1. 移至左側流覽窗格中的 [服務], 並在 "Azure Active Directory" 上執行時鐘
1. 使用功能表中的 [應用程式註冊], 建立「Web 應用程式」並遵循嚮導。 **請記住您在此處建立的名稱**。 您必須將此名稱新增至您的 ADLS 帳戶, 以獲得授權的使用者。
1. 建立 web 應用程式之後, 請在應用程式的 [設定] 下, 移至 [金鑰]。
1. 選取 [金鑰持續時間], 然後按一下 [儲存]。 **儲存產生的金鑰。**
1.  回到 [應用程式註冊] 頁面, 然後按一下頂端的 [端點] 按鈕。 **記下「權杖端點」 URL**
1. 您現在應該已針對 OAuth 記下下列專案:

    - 您在步驟3中所建立之 Web 應用程式的「應用程式識別碼」
    - 您在步驟5中剛產生的金鑰
    - 步驟6中的權杖端點

### <a name="adding-the-service-principal-to-your-adls-account"></a>將服務主體新增至您的 ADLS 帳戶

1. 再次移至入口網站, 並開啟您的 ADLS 帳戶, 然後選取左側功能表中的 [存取控制 (IAM)]。
1. 選取 [新增角色指派], 並搜尋您在上述步驟3中建立的名稱 (請注意, 它不會顯示在清單中, 但如果您搜尋完整名稱, 則會找到)。
1. 現在新增「儲存體 Blob 資料參與者 (預覽)」角色。

請等候5-10 分鐘, 再使用認證來進行掛接

### <a name="set-environment-variable-for-oauth-credentials"></a>設定 OAuth 認證的環境變數

在可存取您 big data 叢集的用戶端電腦上開啟命令提示字元。 使用下列格式來設定環境變數:請注意, 認證必須在逗號分隔清單中。 ' Set ' 命令是在 Windows 上使用。 如果您使用 Linux, 請改用 [匯出]。

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>使用存取金鑰來掛接

您也可以使用可在 Azure 入口網站上取得之 ADLS 帳戶的存取金鑰來進行掛接。

 > [!TIP]
   > 如需如何尋找儲存體帳戶存取金鑰 (`<storage-account-access-key>`) 的詳細資訊, 請參閱[查看帳戶金鑰和連接字串](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string)。

### <a name="set-environment-variable-for-access-key-credentials"></a>設定存取金鑰認證的環境變數

1. 在可存取您 big data 叢集的用戶端電腦上開啟命令提示字元。

1. 在可存取您 big data 叢集的用戶端電腦上開啟命令提示字元。 使用下列格式來設定環境變數。 請注意, 認證必須在逗號分隔清單中。 ' Set ' 命令是在 Windows 上使用。 如果您使用 Linux, 請改用 [匯出]。

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a>掛接遠端 HDFS 儲存體

現在您已設定存取金鑰的 MOUNT_CREDENTIALS 環境變數或使用 OAuth, 您可以開始裝載。 下列步驟會將中的遠端 HDFS 儲存體掛接 Azure Data Lake 至您 big Data 叢集的本機 HDFS 儲存體。

1. 使用**kubectl**在您的 big data 叢集中尋找端點**控制器-svc-外部**服務的 IP 位址。 尋找 [**外部 IP**]。

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 使用具有叢集使用者名稱和密碼的控制器端點的外部 IP 位址, 以**azdata**登入:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. 設定環境變數 MOUNT_CREDENTIALS (滾動以取得指示)

1. 使用**azdata bdc 存放集區掛接建立**, 在 Azure 中掛接遠端 HDFS 儲存體。 執行下列命令之前, 請先取代預留位置值:

   ```bash
   azdata bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
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
