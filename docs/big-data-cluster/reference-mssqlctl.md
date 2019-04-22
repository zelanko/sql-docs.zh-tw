---
title: mssqlctl 參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b050638ee0ca600c5df0ecdbe5616b801f41e7a8
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860350"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**mssqlctl**工具[SQL Server 2019 巨量資料叢集 （預覽）](big-data-cluster-overview.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [app](reference-mssqlctl-app.md) | 建立、 刪除、 執行和管理應用程式。 |
| [cluster](reference-mssqlctl-cluster.md) | 選取、 管理和操作叢集。 |
| [login](#login) | 叢集登入。 |
| [logout](#logout) | 記錄移出叢集。 |
| [storage](reference-mssqlctl-storage.md) | 管理叢集存放裝置。 |

## <a id="login"></a> mssqlctl login

叢集登入。

```
mssqlctl login
   --endpoint
   --password
   --username
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
|**--endpoint -e**| 叢集主機和連接埠 （例如） `http://host:port"`。 |
|**--password -p**| 密碼認證。 |
|**--username -u**| 帳戶的使用者。 |

### <a name="examples"></a>範例

以互動方式登入。

```
mssqlctl login
```

使用者名稱和密碼登入。

```
mssqlctl login -u johndoe@contoso.com -p VerySecret
```

登入使用者名稱、 密碼和叢集端點。

```
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```

## <a id="logout"></a> mssqlctl logout

記錄移出叢集。

```
mssqlctl logout
   --username
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--username -u** | 帳戶使用者，如果遺漏，登出目前使用中的帳戶。 |

### <a name="examples"></a>範例

登出這位使用者。

```
mssqlctl logout --username admin
```

## <a name="next-steps"></a>後續步驟

如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。