---
title: SQL Server 巨量資料叢集的 HDFS 階層處理權限
titleSuffix: Manage HDFS tiering permissions for SQL Server Big Data Clusters
description: 在 SQL Server 巨量資料叢集上管理 HDFS 階層處理的安全性，例如其他 Linux 系統上的權限。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 758338618a312d8efe92503581ae82d49d353e51
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73531968"
---
# <a name="manage-hdfs-permissions-for-big-data-clusters-2019"></a>管理 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的 HDFS 權限

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以 HDFS 作為檔案系統類似於使用 POSIX 取得檔案權限的 Linux 檔案系統。 除了傳統 POSIX 權限模型，HDFS 也支援 POSIX 存取控制清單 (ACL)。 如需詳細資訊，請參閱[有關 ACL 的 Apache Hadoop 文章](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_.28Access_Control_Lists.29)。

下列各節提供如何使用 `azdata` CLI 來管理 HDFS 檔案和目錄權限的範例。

## <a name="prerequisites"></a>Prerequisites

- [部署巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
  
## <a name="hdfs-shell"></a>HDFS 殼層

`azdata` 中的 `hdfs` 殼層功能可讓您直接在殼層中發出命令，以管理 HDFS 檔案和目錄權限。 其基礎機制使用 WebHdfs 呼叫來發出命令

下列命令會開啟殼層。

```bash
azdata bdc hdfs shell
```

若要存取 `hdfs` 殼層的說明，並了解如何發出命令，請在啟用殼層後執行下列命令。

```bash
[hdfs] ?
```

下列範例示範如何建立目錄、列出目錄及修改目錄權限，並為具名使用者 `bob` 提供 `sales` 目錄的讀取、寫入和執行權限。

```bash
[hdfs] mkdir sales
[hdfs] ls
rwxr-xr-x  hdfs bdcadmins        0 Oct 09 18:02 system/
rwxrwxr-x admin bdcadmins        0 Oct 10 16:47 sales/
--xrwxrwxrwx  hdfs bdcadmins        0 Oct 09 18:03 tmp/
rwxrwxrwx  hdfs bdcadmins        0 Oct 09 17:59 user/

[hdfs] acl modify  '/sales/' 'user:bob:rwx'
acl modify: Change completed.
[hdfs] acl status  '/sales/'
{
  `AclStatus`: {
    `entries`: [
      `user:bob:rwx`,
      `group::r-x`
    ],
    `group`: `bdcadmins`,
    `owner`: `admin`,
    `permission`: `775`,
    `stickyBit`: false
  }
}
```

## <a name="create-a-directory-in-hdfs-using-azdata"></a>使用 `azdata` 在 HDFS 中建立目錄

在路徑 `/sales` 中建立名為 `data` 的目錄。

```bash
azdata bdc hdfs mkdir --path '/sales/data'
```

## <a name="change-owner-of-a-directory-or-file"></a>變更目錄或檔案擁有者

變更 HDFS 中 `data` 目錄的擁有使用者，並將 *`alice`* 設為擁有使用者及將 *`salesgroup`* 設為擁有群組。 您本身必須是擁有者，才能變更擁有者。

```bash
azdata bdc hdfs chown --owner alice --group 'salesgroup' --path '/sales/data'
```

## <a name="change-permissions-of-a-file-or-directory-with-chmod"></a>使用 `chmod` 來變更檔案或目錄權限

您可以使用 `chmod` 來變更擁有者、擁有群組及其他人的檔案和目錄權限。 如需詳細資訊，請參閱[變更 Linux 檔案系統上的權限](https://www.lifewire.com/uses-of-command-chmod-2201064)。 在 HDFS 中，模式會相同。 例如：

```bash
azdata bdc hdfs chmod --permission 750 --path /sales/data
```

```bash
azdata bdc hdfs chmod --permission 775 --path /sales/data/file.txt
```

## <a name="set-sticky-bit-on-directories"></a>在目錄上設定黏性位元 (Sticky Bit)

在目錄上設定黏性位元可防止意外刪除或重新配置檔案。 黏性位元會限制超級使用者、目錄擁有者或檔案擁有者才有權刪除或移動檔案。 此設定不會影響檔案。 下列範例藉由在權限前面加上 `1`，以在目錄 `users` 上設定黏性位元。

```bash
azdata bdc hdfs chmod --path /sales/users --permission 1750
```

## <a name="setting-acls-on-files-and-directories"></a>在檔案和目錄上設定 ACL

若要在 HDFS 的檔案和目錄上設定 ACL，請使用 `azdata` 命令。

在目錄上設定 ACL，並為具名使用者 *`tom`* 提供 *`data`* 目錄的讀取、寫入和執行權限。 

> [!NOTE]
> 使用 `set` 命令時，請確定您提供的是完整 ACL 規格，包括擁有使用者、擁有群組及其他人的 ACL 規格。

```bash
azdata bdc hdfs acl set --path '/sales' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-'
```

## <a name="default-acl-on-directories"></a>目錄上的預設 ACL

預設 ACL 可讓子目錄繼承上層目錄的權限。 只有目錄可以有預設 ACL。 建立新檔案或子目錄時，會自動將其父系的預設 ACL 繼承到自己的存取 ACL 中。 如此一來，在建立新的子目錄時，就會在任意深度的目錄層級中往下繼承預設 ACL。

以下示範如何使用 azdata 來設定預設 ACL。

```bash
azdata bdc hdfs acl set --path '/sale' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-,default:group::rw-,default:user::rw-,default:other::rw-'
```

## <a name="next-steps"></a>後續步驟

- [`azdata` 參考](reference-azdata.md)

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
