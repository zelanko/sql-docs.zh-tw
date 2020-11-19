---
title: 變更預設的 R 或 Python 語言執行階段版本
description: 了解如何變更 SQL 執行個體用於 SQL Server 2017 機器學習服務或 SQL Server R Services 的 R 或 Python 執行階段預設版本。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/14/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 457d728bd0e4abb5c2cf70063c0330924104c482
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869974"
---
# <a name="change-the-default-r-or-python-language-runtime-version"></a>變更預設的 R 或 Python 語言執行階段版本

[!INCLUDE[SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

本文說明如何變更 [SQL Server 2016 R Services](../r/sql-server-r-services.md) 或 [SQL Server 2017 機器學習服務](../sql-server-machine-learning-services.md)中使用的 R 或 Python 預設版本。

以下列出不同 SQL Server 版本所包含的 R 和 Python 執行階段版本。

| SQL Server 版本 | 服務 | 累計更新 | R 執行階段版本 | Python 執行階段版本 |
|-|-|-|-|-|
| SQL Server 2016 | R 服務 | RTM - SP2 CU13 | 3.2.2 | 尚未提供 |
| SQL Server 2016 | R 服務 | SP2 CU14 和更新版本 | 3.2.2 和 3.5.2 | 尚未提供 |
| SQL Server 2017 | 機器學習服務 | RTM - CU21 | 3.3.3 | 3.5.2 |
| SQL Server 2017 | 機器學習服務 | CU22 和更新版本 | 3.3.3 和 3.5.2 | 3.5.2 和 3.7.2 |

## <a name="prerequisites"></a>先決條件

您必須安裝累積更新 (CU) 以變更預設的 R 或 Python 語言執行階段版本：

- **SQL Server 2016：** Services Pack (SP) 2 累積更新 (CU) 14 或更新版本
- **SQL Server 2017：** 累積更新 (CU) 22 或更新版本

若要下載最新的累積更新，請參閱[適用於 Microsoft SQL Server 的最新更新](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)。

> [!NOTE]
> 如果您匯集了具有 SQL Server 新安裝的累積更新，將只會安裝最新版本的 R 和 Python 執行階段。

## <a name="change-r-runtime-version"></a>變更 R 執行階段版本

如果您已安裝 SQL Server 2016 或 2017 的上述其中一個累積更新，您的 SQL 執行個體中可能會有多個 R 版本。 每個版本分別包含在執行個體資料夾的子資料夾中，名稱為 `R_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* (原始安裝的資料夾可能不會將版本號碼附加至資料夾名稱)。

如果您安裝了包含 R 3.5 的 CU，新的 `R_SERVICES` 資料夾將是：

- SQL Server 2016：`C:\Program Files\Microsoft SQL Server\MSSQL13.<INSTANCE_NAME>\R_SERVICES.3.5`
- SQL Server 2017：`C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\R_SERVICES.3.5`

每個 SQL 執行個體都會使用其中一個版本作為 R 的預設版本。您可以使用 **RegisterRext.exe** 命令列公用程式來變更預設版本。 公用程式位於每個 SQL 執行個體的 R 資料夾底下：

*&lt;SQL 執行個體路徑&gt;* \R_SERVICES.n.n\library\RevoScaleR\rxLibs\x64\RegisterRext.exe

> [!Note]
> 本文說明的功能僅適用於 SQL CU 中包含的 **RegisterRext.exe** 複本。 請勿使用原始 SQL 安裝隨附的複本。

若要變更 R 執行階段版本，請將下列命令列引數傳遞至 **RegisterRext.exe**：

- `/configure` - 必要，指定您要設定預設的 R 版本。

- `/instance:`*&lt;執行個體名稱&gt;* - (選擇性) 您要設定的執行個體。 若未指定，則會設定預設執行個體。

- `/rhome:`*&lt;R_SERVICES[n.n] 資料夾的路徑&gt;* - 選擇性，您要設定為預設 R 版本的執行階段版本資料夾的路徑。

  如果您未指定 /rhome，則設定的路徑將是 **RegisterRext.exe** 所在的路徑。

### <a name="examples"></a>範例

以下範例說明如何變更 SQL Server 2016 和 2017 中的 R 執行階段版本。

#### <a name="change-r-runtime-version-in-sql-server-2016"></a>變更 SQL Server 2016 中的 R 執行階段版本

例如，若要將 **R 3.5** 設定為 SQL Server 2016 上的執行個體 MSSQLSERVER01 的 R 預設版本：

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

#### <a name="change-r-runtime-version-in-sql-server-2017"></a>變更 SQL Server 2017 中的 R 執行階段版本

例如，若要將 **R 3.5** 設定為 SQL Server 2017 上的執行個體 MSSQLSERVER01 的 R 預設版本：

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

在這些範例中，您無須包含 `/rhome` 引數，因為您指定了 **RegisterRext.exe** 所在的相同資料夾。

## <a name="change-python-runtime-version"></a>變更 Python 執行階段版本

如果您已安裝 SQL Server 2017 的 CU22 或更新版本，您的 SQL 執行個體中可能會有多個 Python 版本。 每個版本分別包含在執行個體資料夾的子資料夾中，名稱為 `PYTHON_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* (原始安裝的資料夾可能不會將版本號碼附加至資料夾名稱)。

例如，如果您安裝了包含 Python 3.7 的 CU，則會建立新的 `PYTHON_SERVICES` 資料夾：

`C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\PYTHON_SERVICES.3.7`  

每個 SQL 執行個體都會使用其中一個版本作為 Python 的預設版本。 您可以使用 **RegisterRext.exe** 命令列公用程式來變更預設版本。 公用程式位於每個 SQL 執行個體的 Python 資料夾底下：

*&lt;SQL 執行個體路徑&gt;* `\PYTHON_SERVICES.n.n\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.exe`

> [!Note]
> 本文說明的功能僅適用於 SQL CU 中包含的 **RegisterRExt.exe** 複本。 請勿使用原始 SQL 安裝隨附的複本。

若要變更 Python 執行階段版本，請將下列命令列引數傳遞至 **RegisterRext.exe**：

- `/configure` - 必要，指定您要設定預設的 Python 版本。

- `/python` - 指定您要設定預設的 Python 版本。 如果您指定 `/pythonhome`，則為選擇性。

- `/instance:`*&lt;執行個體名稱&gt;* - (選擇性) 您要設定的執行個體。 若未指定，則會設定預設執行個體。

- `/pythonhome:`*&lt;PYTHON_SERVICES[n.n] 資料夾的路徑&gt;* - 選擇性，您要設定為預設 Python 版本的執行階段版本資料夾的路徑。

  如果您未指定 /pythonhome，則設定的路徑將是 **RegisterRExt.exe** 所在的路徑。

### <a name="example"></a>範例

例如，若要將 **Python 3.7** 設定為 SQL Server 2017 上的執行個體 MSSQLSERVER01 的 Python 預設版本：

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7\Lib\site-packages\revoscalepy\rxLibs"

.\RegisterRext.exe /configure /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

在此範例中，您無須包含 `/pythonhome` 引數，因為您指定了 **RegisterRext.exe** 所在的相同資料夾。

## <a name="remove-a-runtime-version"></a>移除執行階段版本

若要移除 R 或 Python 版本，請使用 **RegisterRext.exe** 搭配 `/cleanup` 命令列引數 (請使用前述的相同 `/rhome`、`/pythonhome` 和 `/instance` 引數)。

例如，若要從執行個體 MSSQLSERVER01 中移除 **R 3.2** 資料夾：

```cmd
.\RegisterRext.exe /cleanup /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES" /instance:MSSQLSERVER01
```

例如，若要從執行個體 MSSQLSERVER01 中移除 **Python 3.7** 資料夾：

```cmd
.\RegisterRExt.exe /cleanup /python /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

**RegisterRext.exe** 會要求您確認是否要清除指定的 R 執行階段：

> *您確定要永久刪除指定的執行階段及其上安裝的所有套件嗎？\[是(Y)/否(N)/預設值(是)\]：*

若要確認，請回答 `Y`，或按 Enter 鍵。 或者，您也可以在 `/cleanup` 選項中傳入 `/y` 或 `/Yes`，以略過此提示。

> [!NOTE]
> 只有在版本未設定為預設值，且目前並未用來執行 **RegisterRext.exe** 時，您才能移除該版本。

## <a name="next-steps"></a>後續步驟

- [取得 R 套件資訊](../package-management/r-package-information.md)
- [取得 Python 套件資訊](../package-management/python-package-information.md)
- [使用 R 工具來安裝套件](../package-management/install-r-packages-standard-tools.md)
- [使用 Python 工具來安裝套件](../package-management/install-python-packages-standard-tools.md)
