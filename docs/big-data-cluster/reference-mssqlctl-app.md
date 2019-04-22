---
title: mssqlctl 應用程式參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 應用程式命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b418f1ded8d9911143b431ae9793c467c4e26eb4
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860649"
---
# <a name="mssqlctl-app"></a>mssqlctl app

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**應用程式**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [create](#create) | 建立應用程式。 |
| [delete](#delete) | 刪除應用程式。 |
| [describe](#describe) | 說明應用程式。 |
| [init](#init) | 新應用程式基本架構著手進行。 |
| [list](#list) | 列出應用程式。 |
| [run](#run) | 執行應用程式。 |
| [update](#update) | 更新應用程式。 |
| [template](reference-mssqlctl-app-template.md) | 範本的命令。 |

## <a id="create"></a> mssqlctl 應用程式建立

建立應用程式。

```
mssqlctl app create
   --assets
   --code
   --description
   --entrypoint
   --inputs
   --name
   --outputs
   --runtime
   --spec
   --version
   --yes
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--assets -a** | 要包含的其他應用程式檔案資產清單。 |
| **--code -c** | R 或 Python 程式碼檔案路徑。 |
| **--description -d** | 應用程式的說明。 |
| **--entrypoint** |  |
| **--inputs** | 輸入的參數的結構描述。 |
| **--name -n** | 應用程式名稱 |
| **--outputs** | 輸出參數的結構描述。 |
| **--runtime -r** | 應用程式執行階段。  允許的值：Mleap, Python, R, SSIS. |
| **--spec -s** | 描述應用程式的 YAML 規格的檔案與目錄路徑。 |
| **--version -v** | 應用程式版本。 |
| **-是-y** | 不提示確認時從 CWD spec.yaml 檔案建立應用程式。 |

### <a name="examples"></a>範例

建立新的應用程式，透過 spec.yaml （建議選項）。

```
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```

建立新的 Python 應用程式內嵌，使用引數。

```
mssqlctl app create --name add --version v1 --inputs x=float, y=float --outputs result=float --runtime Python --code add.py  --init init.py
```

建立新的 R 應用程式內嵌，使用引數。

```
mssqlctl app create --name add --version v1 --inputs x=numeric, y=numeric --outputs result=numeric --runtime R --code add.R  --init init.R
```

使用要包含的其他檔案資產中建立新的 R 應用程式內嵌。

```
mssqlctl app create --name add --version v1 --runtime R --code  add.R --assets file.RData,/path/to/more/files
```

## <a id="delete"></a> mssqlctl app delete

刪除應用程式。

```
mssqlctl app delete
   --name
   --version
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--name -n** | 應用程式名稱 |
| **--version -v** | 應用程式版本。 |

### <a name="examples"></a>範例

刪除應用程式的名稱和版本。

```
mssqlctl app delete --name reduce --version v1
```

## <a id="describe"></a> mssqlctl app describe

說明應用程式。

```
mssqlctl app describe
   --name
   --spec
   --version
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--name -n** | 應用程式名稱 |
| **--spec -s** | 描述應用程式的 YAML 規格的檔案與目錄路徑。 |
| **--version -v** | 應用程式版本。 |

### <a name="examples"></a>範例

描述應用程式。

```
mssqlctl app describe --name reduce --version v1
```

## <a id="init"></a> mssqlctl 應用程式初始化

新應用程式基本架構著手進行。

```
mssqlctl app init
   --destination
   --name
   --spec
   --template
   --url
   --version
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--destination -d** | 放置應用程式基本架構的位置。 預設： 目前的工作目錄。 |
| **--name -n** | 應用程式名稱 |
| **--spec -s** | 產生只是應用程式 spec.yaml。 |
| **--template -t** | 範本名稱。 如需完整的清單，支援的範本名稱關閉執行`mssqlctl app template list`。 |
| **--url -u** | 指定不同的範本存放庫位置。 預設值： https://github.com/Microsoft/sql-server-samples.git。 |
| **--version -v** | 應用程式版本。 |

### <a name="examples"></a>範例

建立新的應用程式的結構`spec.yaml`只。

```
mssqlctl app init --spec
```

建立新 R 應用程式的應用程式基本架構為基礎的結構`r`範本。

```
mssqlctl app init --name reduce --template r
```

建立新 Python 應用程式的應用程式基本架構為基礎的結構`python`範本。

```
mssqlctl app init --name reduce --template python
```

建立新 SSIS 應用程式的應用程式基本架構為基礎的結構`ssis`範本。

```
mssqlctl app init --name reduce --template ssis
```

## <a id="list"></a> mssqlctl app list

列出應用程式。

```
mssqlctl app list
   --name
   --version
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--name -n** | 應用程式名稱 |
| **--version -v** | 應用程式版本。 |

### <a name="examples"></a>範例

列出依名稱和版本的應用程式。

```
mssqlctl app list --name reduce  --version v1
```

依名稱列出所有的應用程式版本。

```
mssqlctl app list --name reduce
```

列出所有的應用程式。

```
mssqlctl app list
```

## <a id="run"></a> mssqlctl app run

執行應用程式。

```
mssqlctl app run
   --name
   --version
   --inputs
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--name -n** | 應用程式名稱 |
| **--version -v** | 應用程式版本。 |
| **--inputs** | 應用程式中的輸入參數 CSV`name=value`格式。 |

### <a name="examples"></a>範例

執行應用程式不含輸入參數。

```
mssqlctl app run --name reduce --version v1
```

執行應用程式與 1 個輸入參數。

```
mssqlctl app run --name reduce --version v1 --inputs x=10
```

執行應用程式與多個輸入參數。

```
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6
```

## <a id="update"></a> mssqlctl app update

更新應用程式。

```
mssqlctl app update
   --spec
   --yes
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--spec -s** | 描述應用程式的 YAML 規格的檔案與目錄路徑。 |
| **-是-y** | 不提示確認時從 CWD spec.yaml 檔案將應用程式更新。 |

## <a name="next-steps"></a>後續步驟

如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。