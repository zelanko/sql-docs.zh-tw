---
title: 預設 R 和 Python 封裝程式庫
description: R 和 Python 套件由 R Services、R Server、Machine Learning Services (資料庫內) 和 Machine Learning Server (獨立式) 的 SQL Server 所安裝
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e49b843b0b32969bd440177cf445916487ad2670
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715206"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server 中的預設 R 和 Python 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文列出隨 SQL Server 安裝的 R 和 Python 套件, 以及要在哪裡尋找封裝程式庫。  

## <a name="r-package-list-for-sql-server"></a>SQL Server 的 R 封裝清單

當您在安裝期間選取 R 功能時, r 封裝會與[SQL Server 2016 R 服務](../install/sql-r-services-windows-install.md)一起安裝, 並[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。 

|Packages         | 2016 | 2017 | 描述 |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 用於遠端計算內容、串流、平行執行 rx 函數以進行資料匯入和轉換、模型化、視覺化和分析。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |用於包含預存程式中的 R 腳本。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 馬丁 | 9.2 | 在 R 中新增機器學習演算法。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 馬丁  | 9.2 | 用於在 R 中撰寫 MDX 語句。 |

SQL Server Machine Learning 服務中預設會提供 MicrosoftML 和 olapR。 在 SQL Server 2016 R Services 實例上, 您可以透過[元件升級](../install/upgrade-r-and-python.md)來新增這些封裝。 元件升級也會取得較新版本的套件 (例如, 較新版本的 RevoScaleR 包含 SQL Server 上封裝管理的功能)。

## <a name="python-package-list-for-sql-server"></a>SQL Server 的 Python 套件清單

只有當您安裝[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)並選取 python 功能時, python 套件才會在 SQL Server 2017 中提供。

| Packages         | 2017    |  描述 |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用於遠端計算內容、串流、平行執行 rx 函數以進行資料匯入和轉換、模型化、視覺化和分析。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 在 Python 中新增機器學習演算法。 |

## <a name="open-source-r-in-your-installation"></a>安裝中的開放原始碼 R

R 支援包含開放原始碼, 因此您可以呼叫基底 R 函式, 並安裝其他開放原始碼和協力廠商套件。 R 語言支援包括**基底**、**統計**資料、 **utils**及其他等核心功能。 R 的基礎安裝也包含多個範例資料集和標準 R 工具, 例如**rgui.exe** (輕量互動式編輯器) 和**RTerm** (R 命令提示字元)。 

安裝中包含的開放原始碼 R 散發是[Microsoft R open (MRO)](https://mran.microsoft.com/open)。 MRO 會包含其他開放原始碼套件 (例如[Intel Math 核心程式庫](https://en.wikipedia.org/wiki/Math_Kernel_Library)), 以將值新增至基底 R。

下表摘要說明 MRO 使用 SQL Server 安裝程式所提供的 R 版本。

|版本             | R 版本       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

您絕對不應該以 web 上的較新版本, 手動覆寫 SQL Server 安裝程式所安裝的 R 版本。 Microsoft R 套件是以特定版本的 R 為基礎。修改您的安裝可能會使其變得不穩定。

## <a name="open-source-python-in-your-installation"></a>安裝中的開放原始碼 Python

SQL Server 2017 新增 Python 元件。 當您選取 [Python 語言] 選項時, 會安裝 Anaconda 4.2 散發套件。 除了 Python 程式碼程式庫, 標準安裝還包含範例資料、單元測試和範例腳本。 

SQL Server 2017 Machine Learning 是支援 R 和 Python 的第一版。

|版本             | Anaconda 版本| Microsoft 套件    |
|--------------------|-----------------|-----------------------|
| SQL Server 機器學習服務  | 4.2 over Python 3。5 | revoscalepy、microsoftml |

您絕對不應該手動覆寫 web 上的更新版本 SQL Server 安裝程式所安裝的 Python 版本。 Microsoft Python 套件是以特定版本的 Anaconda 為基礎。 修改您的安裝可能不穩定。

## <a name="component-upgrades"></a>元件升級

初始安裝之後, R 和 Python 套件會透過 service pack 和累積更新進行重新整理, 但只有系結至新式生命週期支援原則, 才能進行完整版本升級。 系結會變更服務模型。 根據預設, 在初始安裝之後, R 封裝會透過 service pack 和累計更新進行重新整理。 只有透過產品升級 (從 SQL Server 2016 到 SQL Server 2017) 或將 R 支援系結至 Microsoft Machine Learning Server, 才能夠進行核心 R 元件的其他套件和完整版本升級。 如需詳細資訊, 請參閱[在 SQL Server 中升級 R 和 Python 元件](../install/upgrade-r-and-python.md)。

## <a name="package-library-location"></a>封裝程式庫位置

當您使用 SQL Server 安裝機器學習服務時, 系統會針對您安裝的每個語言, 在實例層級建立單一套件程式庫。 在 Windows 上, 實例程式庫是向 SQL Server 註冊的安全資料夾。

在 SQL Server 上執行的所有腳本或程式碼, 都必須從實例程式庫載入函數。 SQL Server 無法存取已安裝到其他程式庫的套件。 這也適用于遠端用戶端。 從遠端用戶端連接到伺服器時, 任何您想要在伺服器計算內容中執行的 R 或 Python 程式碼, 都只能使用安裝在實例程式庫中的套件。

若要保護伺服器資產, 預設實例庫只能由電腦系統管理員修改。 如果您不是電腦的擁有者, 您可能需要取得系統管理員的許可權, 才能將套件安裝到此程式庫。 

#### <a name="file-path-for-in-database-engine-instances"></a>資料庫內引擎實例的檔案路徑

下表顯示 R 和 Python 的檔案位置, 適用于版本和資料庫引擎實例組合。 MSSQL13.MSSQLSERVER 表示 SQL Server 2016, 而且是僅限 R。 MSSQL14. 表示 SQL Server 2017, 並具有 R 和 Python 資料夾。 

檔案路徑也包括實例名稱。 SQL Server 會將[資料庫引擎實例](../../database-engine/configure-windows/database-engine-instances-sql-server.md)安裝為預設實例 (MSSQLSERVER) 或使用者定義的已命名實例。 如果 SQL Server 安裝為已命名的實例, 您會看到該名稱附加如下: `MSSQL13.<instance_name>`。

|版本和語言  | 預設路徑|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library|
| 使用 R 的 SQL Server 2017|C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |
| 使用 Python SQL Server 2017 |C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>獨立伺服器安裝的檔案路徑

下表列出安裝 SQL Server 2016 R Server (獨立式) 或 SQL Server 2017 Machine Learning Server (獨立式) 伺服器時, 二進位檔的預設路徑。 

|Version| 安裝|預設路徑|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server, 使用 R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, 使用 Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果您發現其他資料夾具有類似的子資料夾名稱和檔案, 您可能會有獨立安裝的 Microsoft R Server 或[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)。 這些伺服器產品有不同的安裝程式和路徑 (亦即, C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER)。 如需詳細資訊, 請參閱[安裝適用于 windows 的 Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或[安裝適用于 Windows 的 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="next-steps"></a>後續步驟

+ [取得封裝資訊](installed-package-information.md)
+ [安裝新的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [啟用遠端 R 封裝管理](../r/r-package-how-to-enable-or-disable.md)
+ [適用於 R 封裝管理的 RevoScaleR 函式](../r/use-revoscaler-to-manage-r-packages.md)
+ [R 封裝同步處理](../r/package-install-uninstall-and-sync.md)
+ [本機 R 封裝存放庫的 miniCRAN](../r/create-a-local-package-repository-using-minicran.md)
