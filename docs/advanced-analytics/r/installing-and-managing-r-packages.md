---
title: 預設 SQL Server R 和 SQL Server 機器學習中的 R，並將 Python 封裝程式庫 |Microsoft 文件
description: SQL Server R 服務，R Server 機器學習服務 （資料庫），與機器學習伺服器 （獨立） 所安裝的 R，並將 Python 封裝
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9362d6e9dc98f80beabc301f43e755b205b40a10
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707286"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>在 SQL Server 中的預設 R，並將 Python 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文列出與 SQL Server 以及如何尋找封裝程式庫一起安裝的 R，並將 Python 封裝。  

## <a name="r-package-list-for-sql-server"></a>SQL Server 的 R 封裝清單

安裝 R 封裝與[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)和[SQL Server 2017 機器學習服務](../install/sql-machine-learning-services-windows-install.md)當您在安裝期間選取 R 功能。 

Packages         | 2016 | 2017 | 描述 |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 用於遠端計算內容資料流的資料匯入和轉換、 模型、 視覺化和分析 rx 函式的平行執行。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |使用預存程序包括 R 指令碼。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | 新增機器學習演算法中。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | 用於在 r 中撰寫 MDX 陳述式 |

MicrosoftML 和 olapR 可用預設會在 SQL Server 2017 機器學習服務。 SQL Server 2016 R 服務執行個體上，您可以加入到這些封裝[元件升級](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 元件升級也會取得您的封裝的較新版本 （例如，較新版本的 RevoScaleR 包含函式的 SQL Server 上的封裝管理）。

## <a name="python-package-list-for-sql-server"></a>SQL Server 的 Python 封裝清單

在安裝時，僅適用於 SQL Server 2017 Python 封裝所[SQL Server 2017 機器學習服務](../install/sql-machine-learning-services-windows-install.md)並選取 [Python] 功能。

| Packages         | 2017    |  描述 |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用於遠端計算內容資料流的資料匯入和轉換、 模型、 視覺化和分析 rx 函式的平行執行。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 以 Python 新增機器學習演算法。 |

## <a name="open-source-r-in-your-installation"></a>您的安裝中的開放原始碼 R

R 的支援包括開放原始碼，以便您可以呼叫基底 R 函數，並安裝其他的開放原始碼和第三方封裝。 R 語言支援包含核心功能，例如**基底**， **stats**， **utils**，和其他人。 R 的基底安裝也包含許多的範例資料集，以及標準的 R 工具，像是**RGui** （輕量型互動式編輯器） 和**RTerm** （R 命令提示字元）。 

在安裝中包含的開放原始碼 R 的分配[Microsoft R 開啟 (MRO)](https://mran.microsoft.com/open)。 MRO 將值加入至基底 R 所包括的其他開放原始碼套件，例如[Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library)。

下表摘要說明 R MRO 使用 SQL Server 安裝程式所提供的版本。

|版本             | R 版本       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 機器學習服務](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

您應該永遠不會以手動方式覆寫 SQL Server 安裝程式安裝在網站上的較新版本的 R 的版本。 Microsoft R 封裝以特定版本的 r 修改您的安裝可能造成不穩定它。

## <a name="open-source-python-in-your-installation"></a>在您的安裝中的開放原始碼 Python

SQL Server 2017 加入 Python 元件。 當您選取的 Python 語言選項時，安裝 Anaconda 4.2 發佈。 除了 Python 程式碼程式庫，標準安裝包含範例資料、 單元測試及範例指令碼。 

SQL Server 2017 機器學習為 R 和 Python 支援第一次的釋放。

|版本             | Anaconda 版本| Microsoft 封裝    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning 服務  | 4.2 透過 Python 3.5 | revoscalepy microsoftml |

您應該永遠不會以手動方式覆寫 SQL Server 安裝程式安裝在網站上的較新版本的 Python 的版本。 Microsoft Python 封裝為基礎的 Anaconda 特定版本。 修改您的安裝可能造成不穩定它。

## <a name="component-upgrades"></a>元件升級

初始安裝之後，R 和 Python 封裝重新整理透過 service pack 和累計更新，但是完整版本升級時，才可以由*繫結*現代的生命週期支援原則。 繫結變更服務模型。 根據預設，初始安裝之後，R 封裝會重新整理透過 service pack 和累計更新。 其他封裝及核心 R 元件的完整版本升級僅能透過產品升級 （從 SQL Server 2016 到 SQL Server 2017) 或透過繫結 R 支援 Microsoft 機器學習服務伺服器。 如需詳細資訊，請參閱[中 SQL Server 升級 R 和 Python 元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="package-library-location"></a>封裝程式庫位置

當您安裝 SQL server 的機器學習服務時，在您安裝的每種語言的執行個體層級建立單一封裝程式庫。 在 Windows 中，執行個體的程式庫是受保護的資料夾，向 SQL Server。

所有的指令碼或程式碼，執行中的 SQL Server 上資料庫必須從執行個體文件庫載入函式。 SQL Server 無法存取封裝安裝到其他文件庫。 這適用於遠端的用戶端。 從遠端用戶端連線到伺服器，當您想要 server 計算內容中執行任何 R 或 Python 程式碼只能使用安裝執行個體文件庫中的封裝。

若要保護伺服器資產，可以只由電腦管理員修改預設執行個體文件庫。 如果您不是電腦的擁有者，您可能需要從系統管理員才能安裝封裝至這個文件庫中取得的權限。 

#### <a name="file-path-for-in-database-engine-instances"></a>在 Database engine 執行個體的檔案路徑

下表顯示的檔案位置的 R，並將 Python 版本和資料庫引擎執行個體組合。 MSSQL13 表示 SQL Server 2016，並且僅 R。 MSSQL14 指出 SQL Server 2017，而且 R 和 Python 的資料夾。 

檔案路徑也會包含執行個體名稱。 SQL Server 安裝[資料庫引擎執行個體](../../database-engine/configure-windows/database-engine-instances-sql-server.md)當做預設執行個體 (MSSQLSERVER) 或使用者定義的具名執行個體。 如果 SQL Server 安裝為具名執行個體，您會看到該名稱後面附加，如下所示： `MSSQL13.<instance_name>`。

|版本和語言  | 預設路徑|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library|
| R 與 SQL Server 2017|C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 使用 Python |C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Lib\site 封裝 |


#### <a name="file-path-for-standalone-server-installations"></a>獨立伺服器安裝的檔案路徑

安裝 SQL Server 2016 R 伺服器 （獨立） 或 SQL Server 2017 機器學習伺服器 （獨立） 伺服器時下, 表列出的二進位檔的預設路徑。 

|版本| 安裝|預設路徑|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|機器學習服務伺服器，以 R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|機器學習服務伺服器，使用 Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果您發現有類似的子資料夾名稱和檔案的其他資料夾，您可能會有 Microsoft R Server 的獨立安裝或[Machine Learning 伺服器](https://docs.microsoft.com/machine-learning-server/)。 這些伺服器產品有不同的安裝程式與路徑 （也就是 C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER）。 如需詳細資訊，請參閱[安裝機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或[適用於 Windows 安裝 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="next-steps"></a>後續的步驟

+ [取得封裝資訊](determine-which-packages-are-installed-on-sql-server.md)
+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [啟用遠端 R 封裝管理](r-package-how-to-enable-or-disable.md)
+ [適用於 R 封裝管理的 RevoScaleR 函式](use-revoscaler-to-manage-r-packages.md)
+ [R 封裝同步處理](package-install-uninstall-and-sync.md)
+ [本機 R 封裝存放庫的 miniCRAN](create-a-local-package-repository-using-minicran.md)
