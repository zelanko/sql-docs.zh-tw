---
title: 取得 R 封裝資訊
description: 瞭解如何在 SQL Server Machine Learning 服務和 SQL Server R Services 上取得已安裝 R 套件的相關資訊。
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
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641155"
---
# <a name="get-r-package-information"></a>取得 R 封裝資訊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何在 SQL Server Machine Learning 服務和 SQL Server R Services 上取得已安裝 R 套件的相關資訊。 範例 R 腳本會示範如何列出封裝資訊, 例如安裝路徑和版本。

## <a name="default-r-library-location"></a>預設 R 程式庫位置

當您使用 SQL Server 安裝機器學習服務時, 系統會針對您安裝的每個語言, 在實例層級建立單一套件程式庫。 在 Windows 上, 實例程式庫是向 SQL Server 註冊的安全資料夾。

在 SQL Server 的資料庫內執行的所有腳本都必須從實例程式庫載入函數。 SQL Server 無法存取已安裝到其他程式庫的套件。 這也適用于遠端用戶端: 在伺服器計算內容中執行的任何 R 腳本都只能使用安裝在實例程式庫中的封裝。
若要保護伺服器資產, 預設實例庫只能由電腦系統管理員修改。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
R 二進位檔的預設路徑是:

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
R 二進位檔的預設路徑是:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
R 二進位檔的預設路徑是:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

這會採用預設的 SQL 實例 MSSQLSERVER。 如果 SQL Server 安裝為使用者定義的命名實例, 就會改用指定的名稱。

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

執行下列語句, 以確認目前實例的預設 R 封裝程式庫:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

下列語句會使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)來傳回實例程式庫的路徑, 以及 SQL Server 所使用的 RevoScaleR 版本:

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
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函數只能在本機電腦上執行。 函數無法傳回遠端連線的程式庫路徑。

## <a name="default-r-packages"></a>預設 R 封裝

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

下列 R 封裝會與 SQL Server R Services 一併安裝。

|Packages | Version | 描述 |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 用於遠端計算內容、串流、平行執行 rx 函數以進行資料匯入和轉換、模型化、視覺化和分析。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 用於包含預存程式中的 R 腳本。 |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

當您在安裝期間選取 R 功能時, 會使用 SQL Server Machine Learning 服務來安裝下列 R 套件。

|Packages | Version | 描述 |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | 用於遠端計算內容、串流、平行執行 rx 函數以進行資料匯入和轉換、模型化、視覺化和分析。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9.2 | 用於包含預存程式中的 R 腳本。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9.2 | 在 R 中新增機器學習演算法。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9.2 | 用於在 R 中撰寫 MDX 語句。 |

::: moniker-end

### <a name="component-upgrades"></a>元件升級

根據預設, R 封裝會透過 service pack 和累計更新進行重新整理。 核心 R 元件的其他套件和完整版本升級只能透過產品升級, 或藉由將 R 支援系結至 Microsoft Machine Learning Server。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
此外, 您可以透過元件升級, 將 MicrosoftML 和 olapR 封裝新增至 SQL Server 實例。
::: moniker-end

如需詳細資訊, 請參閱[在 SQL Server 中升級 R 和 Python 元件](../install/upgrade-r-and-python.md)。

## <a name="default-open-source-r-packages"></a>預設的開放原始碼 R 套件

R 支援包含開放原始碼, 因此您可以呼叫基底 R 函式, 並安裝其他開放原始碼和協力廠商套件。 R 語言支援包括**基底**、**統計**資料、 **utils**及其他等核心功能。 R 的基礎安裝也包含多個範例資料集和標準 R 工具, 例如**rgui.exe** (輕量互動式編輯器) 和**RTerm** (R 命令提示字元)。

安裝中包含的開放原始碼 R 散發是[Microsoft R open (MRO)](https://mran.microsoft.com/open)。 MRO 會包含其他開放原始碼套件 (例如[Intel Math 核心程式庫](https://en.wikipedia.org/wiki/Math_Kernel_Library)), 以將值新增至基底 R。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
MRO 使用 SQL Server R Services 安裝程式所提供的 R 版本是3.2.2。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
MRO 使用 SQL Server Machine Learning 服務安裝程式所提供的 R 版本是3.3.3。
::: moniker-end

> [!IMPORTANT]
> 您絕對不應該以 web 上的較新版本, 手動覆寫 SQL Server 安裝程式所安裝的 R 版本。 Microsoft R 套件是以特定版本的 R 為基礎。修改您的安裝可能會使其變得不穩定。

## <a name="list-all-installed-r-packages"></a>列出所有已安裝的 R 套件

下列範例會[!INCLUDE[tsql](../../includes/tsql-md.md)]在預存程式`installed.packages()`中使用 r 函數, 以顯示已安裝在目前 SQL 實例的 R_SERVICES 程式庫中的 r 封裝清單。 此腳本會傳回描述檔案中的 [封裝名稱] 和 [版本] 欄位。

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

如需 [R 封裝描述] 欄位之選擇性和預設欄位的詳細資訊, [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)請參閱。

## <a name="find-a-single-r-package"></a>尋找單一 R 套件

如果您已安裝 R 封裝, 而且想要確定它可用於特定的 SQL Server 實例, 您可以執行預存程式來載入封裝並傳回訊息。

例如, 下列語句會尋找並載入[粘附](https://cran.r-project.org/web/packages/glue/)套件 (如果有的話)。
如果找不到或無法載入封裝, 您會收到包含文字的錯誤「沒有名為 ' 粘附 ' 的套件」。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

若要查看套件的詳細資訊, 請`packageDescription`參閱。
下列語句會傳回**粘附**封裝的資訊。

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
+ [R 和 Python 教學課程](../tutorials/machine-learning-services-tutorials.md)
