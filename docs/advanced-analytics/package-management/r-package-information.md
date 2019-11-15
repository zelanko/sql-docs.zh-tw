---
title: 取得 Python 資訊
description: 了解如何取得 SQL Server 機器學習服務和 SQL Server R Services 上已安裝之 R 套件的相關資訊。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8c3cf3c1debc03c169c585521b8b46dd8b1365c5
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641155"
---
# <a name="get-r-package-information"></a>取得 Python 資訊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何取得 SQL Server 機器學習服務和 SQL Server R Services 上已安裝之 R 套件的相關資訊。 範例 R 指令碼會示範如何列出套件資訊，例如安裝路徑與版本。

## <a name="default-r-library-location"></a>預設 R 程式庫位置

搭配 SQL Server 安裝機器學習時，會針對您安裝的每個語言在執行個體層次建立單一套件程式庫。 在 Windows 上，執行個體程式庫是一個向 SQL Server 註冊的受保護資料夾。

所有在 SQL Server 上資料庫內執行的指令碼都必須從執行個體程式庫載入函式。 SQL Server 無法存取安裝至其他程式庫的套件。 這也適用於遠端用戶端：任何在伺服器計算內容中執行的 R 指令碼都只能使用安裝在執行個體程式庫中的套件。
為了保護伺服器資產，只有電腦系統管理員才能修改預設執行個體程式庫。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
R 的二進位檔預設路徑是：

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
R 的二進位檔預設路徑是：

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
R 的二進位檔預設路徑是：

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

這會假設預設 SQL 執行個體 MSSQLSERVER。 如果將 SQL Server 安裝成使用者定義的具名執行個體，則會改用指定的名稱。

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

執行下列陳述式來確認目前執行個體的預設 R 套件程式庫：

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

下列陳述式使用 [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 來傳回 SQL Server 所使用的執行個體程式庫路徑和 RevoScaleR 版本：

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 函式只能在本機電腦上執行。 此函式無法傳回遠端連線的程式庫路徑。

## <a name="default-r-packages"></a>預設 R 套件

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

以下是與 SQL Server R Services 一起安裝的 R 套件。

|Packages | 版本 | Description |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 用於遠端計算內容、串流、平行執行 rx 函式以進行資料匯入與轉換、模型化、視覺化，以及分析。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 用於將 R 指令碼包含在預存程序中。 |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

以下是您在安裝期間選取 R 功能時，與 SQL Server 機器學習服務一起安裝的 R 套件。

|Packages | 版本 | Description |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | 用於遠端計算內容、串流、平行執行 rx 函式以進行資料匯入與轉換、模型化、視覺化，以及分析。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9.2 | 用於將 R 指令碼包含在預存程序中。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9.2 | 在 R 中新增機器學習演算法。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9.2 | 用於在 R 中撰寫 MDX 陳述式。 |

::: moniker-end

### <a name="component-upgrades"></a>元件升級

預設會透過 Service Pack 和累積更新重新整理 R 套件。 額外套件及核心 R 元件的完整版本升級只有透過產品升級或將 R 支援繫結至 Microsoft Machine Learning Server，才可能實現。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
此外，您也可以透過元件升級將 MicrosoftML 和 olapR 套件新增至 SQL Server 執行個體。
::: moniker-end

如需詳細資訊，請參閱[升級 SQL Server 中的 R 和 Python 元件](../install/upgrade-r-and-python.md)。

## <a name="default-open-source-r-packages"></a>預設的開放原始碼 R 套件

R 支援包括開放原始碼 R，因此您可以呼叫基底 R 函式及安裝額外的開放原始碼和協力廠商套件。 R 語言支援包括「基底」  、「統計資料」  、「公用程式」  等核心功能。 R 的基礎安裝也包括眾多範例資料集和標準 R 工具，例如 **RGui** (輕量型互動式編輯器) 和 **RTerm** (R 命令提示字元)。

您安裝中包含的開放原始碼 R 散發套件是 [Microsoft R Open (MRO)](https://mran.microsoft.com/open)。 MRO 會藉由包含額外的開放原始碼套件 (例如[Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library)) 提升基底 R 價值。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
使用 SQL Server R Services 安裝程式之 MRO 所提供的 R 版本為 3.2.2。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
使用 SQL Server Machine Learning Services 安裝程式之 MRO 所提供的 R 版本為 3.3.3。
::: moniker-end

> [!IMPORTANT]
> 您一律不應手動以 Web 上較新的版本覆寫 SQL Server 安裝程式所安裝的 R 版本。 Microsoft R 套件以特定 R 版本為基礎。修改安裝可能使其變得不穩定。

## <a name="list-all-installed-r-packages"></a>列出所有已安裝的 R 套件

下列範例使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中的 R 函式 `installed.packages()`，來顯示已在目前 SQL 執行個體的 R_SERVICES 程式庫中安裝的 R 套件清單。 此指令碼會傳回 DESCRIPTION 檔案中的套件名稱和版本欄位。

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

如需有關 R 套件 DESCRIPTION 欄位中選擇性欄位與預設欄位的詳細資訊，請參閱 [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file) \(英文\)。

## <a name="find-a-single-r-package"></a>尋找單一 R 套件

如果您已安裝 R 套件並想確定特定 SQL Server 執行個體能夠使用它，您可以執行預存程序來載入套件並傳回訊息。

例如，下列陳述式會尋找並載入 [glue](https://cran.r-project.org/web/packages/glue/) 套件 (如果可供使用)。
如果無法找到或載入套件，您就會收到包含「沒有名為 'glue' 的套件」文字的錯誤。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

若要查看有關此套件的詳細資訊，請檢視 `packageDescription`。
下列陳述式會傳回 **glue** 套件的資訊。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>後續步驟

+ [安裝新的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)
+ [取得 Python 套件資訊](python-package-information.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [R 與 Python 教學課程](../tutorials/machine-learning-services-tutorials.md)
