---
title: mssqlctl 參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ebd3b63d641c77dae1afbff21264ec4fe34df4d0
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775496"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**mssqlctl**工具[SQL Server 2019 巨量資料叢集 （預覽）](big-data-cluster-overview.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[mssqlctl 應用程式](reference-mssqlctl-app.md) | 建立、 刪除、 執行和管理應用程式。 |
|[mssqlctl cluster](reference-mssqlctl-cluster.md) | 選取、 管理和操作叢集。 |
[mssqlctl login](#mssqlctl-login) | 叢集登入。
[mssqlctl logout](#mssqlctl-logout) | 記錄移出叢集。
|[mssqlctl storage](reference-mssqlctl-storage.md) | 管理叢集存放裝置。 |
## <a name="mssqlctl-login"></a>mssqlctl 登入
叢集登入。
```bash
mssqlctl login [--username -u] 
               [--password -p]  
               [--endpoint -e]
```
### <a name="examples"></a>範例
以互動方式登入。
```bash
mssqlctl login
```
使用者名稱和密碼登入。
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret
```
登入使用者名稱、 密碼和叢集端點。
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```
### <a name="optional-parameters"></a>選擇性參數
#### `--username -u`
帳戶的使用者。
#### `--password -p`
密碼認證。
#### `--endpoint -e`
叢集主機和連接埠 （例如） 」 http://host:port"。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細程度以顯示所有偵錯記錄檔。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值： json、 jsonc、 table、 tsv。  預設值： json。
#### `--query -q`
JMESPath 查詢字串。 請參閱[ http://jmespath.org/ ](http://jmespath.org/])如需詳細資訊和範例。
#### `--verbose`
增加記錄詳細程度。 使用--debug 取得完整的偵錯記錄。
## <a name="mssqlctl-logout"></a>mssqlctl 登出
記錄移出叢集。
```bash
mssqlctl logout 
```
### <a name="examples"></a>範例
登出這位使用者。
```bash
mssqlctl logout
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細程度以顯示所有偵錯記錄檔。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值： json、 jsonc、 table、 tsv。  預設值： json。
#### `--query -q`
JMESPath 查詢字串。 請參閱[ http://jmespath.org/ ](http://jmespath.org/])如需詳細資訊和範例。
#### `--verbose`
增加記錄詳細程度。 使用--debug 取得完整的偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。