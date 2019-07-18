---
title: 預設 R 和 Python 套件程式庫-SQL Server Machine Learning 服務
description: SQL Server R Services，R 伺服器的 Machine Learning 服務 （資料庫內），與 Machine Learning Server （獨立式） 所安裝的 R 和 Python 套件
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 887bae28ffe35ad006bceb08a1b62b824795be0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962799"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server 中的預設 R 和 Python 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文列出與 SQL Server 和哪裡可以找到的套件程式庫一起安裝的 R 和 Python 套件。  

## <a name="r-package-list-for-sql-server"></a>適用於 SQL Server 的 R 套件清單

R 封裝會隨[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)並[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)當您在安裝期間選取 [R] 功能。 

|Packages         | 2016 | 2017 | 描述 |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 使用遠端計算內容，資料流的資料匯入和轉換、 模型、 視覺化和分析的 rx 函式的平行執行。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |使用預存程序包括 R 指令碼。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 荷屬安地列斯 | 9.2 | 將的機器學習服務演算法 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 荷屬安地列斯  | 9.2 | 使用 r 中撰寫 MDX 陳述式 |

MicrosoftML 及 olapR 可根據預設，在 SQL Server 2017 Machine Learning 服務。 在 SQL Server 2016 R Services 執行個體中，您可以將透過這些封裝[元件升級](../install/upgrade-r-and-python.md)。 元件升級也會取得您較新版的套件 （例如，RevoScaleR 的較新版本包含 SQL Server 上的套件管理的函式）。

## <a name="python-package-list-for-sql-server"></a>適用於 SQL Server 的 Python 套件清單

當您安裝 Python 套件是僅適用於 SQL Server 2017 [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，然後選取 [Python] 功能。

| Packages         | 2017    |  描述 |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 使用遠端計算內容，資料流的資料匯入和轉換、 模型、 視覺化和分析的 rx 函式的平行執行。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 在 Python 中新增機器學習服務演算法。 |

## <a name="open-source-r-in-your-installation"></a>您的安裝中的開放原始碼 R

R 支援包括開放原始碼，您可以呼叫基底 R 函數，並安裝其他的開放原始碼和第三方套件。 R 語言支援包含核心功能，例如**基底**， **stats**， **utils**，和其他人。 R 的基底安裝也包含許多範例資料集，以及標準的 R 工具，例如**RGui** （一種輕量型的互動式編輯器） 和**RTerm** （R 命令提示字元）。 

在安裝中包含的開放原始碼 R 的分佈[Microsoft R 開啟 (MRO)](https://mran.microsoft.com/open)。 MRO 將值加入至基底 R 所包括的其他開放原始碼套件，例如[Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library)。

下表摘要說明使用 SQL Server 安裝程式的 MRO 所提供的 R 版本。

|版本             | R 版本       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

您應該永遠不會以手動方式覆寫 SQL Server 安裝程式安裝在網站上的較新版本的 R 的版本。 Microsoft R 套件以在特定版本的 r 修改您的安裝可能造成不穩定它。

## <a name="open-source-python-in-your-installation"></a>您的安裝中的開放原始碼 Python

SQL Server 2017 新增 Python 元件。 當您選取 [Python 語言] 選項時，會安裝 Anaconda 4.2 發佈。 Python 程式碼程式庫，除了標準安裝包含範例資料、 單元測試和範例指令碼。 

SQL Server 2017 Machine Learning 是第一個版本，具有 R 和 Python 支援。

|版本             | Anaconda 版本| Microsoft 封裝    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning 服務  | 4.2 透過 Python 3.5 | revoscalepy microsoftml |

您應該永遠不會以手動方式覆寫 SQL Server 安裝程式安裝在網站上的較新版本的 Python 的版本。 Microsoft 的 Python 套件是以特定版本的 Anaconda 為根據。 修改您的安裝可能造成不穩定它。

## <a name="component-upgrades"></a>元件升級

初始安裝之後，R 和 Python 套件會重新整理透過 service pack 和累計更新，但完整的版本升級時，才可以藉由*繫結*新式生命週期支援原則。 繫結變更服務模型。 根據預設，初始安裝之後，R 封裝會重新整理透過 service pack 和累計更新。 其他封裝及 R 核心元件的完整版本升級只能透過產品升級 （從 SQL Server 2017 的 SQL Server 2016)，或藉由繫結 R 支援 Microsoft Machine Learning Server。 如需詳細資訊，請參閱 < [SQL Server 中的升級 R 和 Python 元件](../install/upgrade-r-and-python.md)。

## <a name="package-library-location"></a>封裝程式庫位置

當您安裝機器學習服務與 SQL Server 時，會將單一套件程式庫建立執行個體層級針對每個您所安裝的語言。 在 Windows 中，執行個體文件庫會是受保護的資料夾，使用 SQL Server 註冊。

所有的指令碼或程式碼，執行在資料庫上 SQL Server 必須從執行個體文件庫載入函式。 SQL Server 無法存取其他程式庫安裝的套件。 這適用於遠端的用戶端。 從遠端用戶端連線到伺服器，當您想要在伺服器計算內容中執行任何 R 或 Python 程式碼只能使用執行個體文件庫中安裝套件。

若要保護伺服器資產，可以修改預設執行個體的程式庫只能由電腦系統管理員。 如果您不是電腦的擁有者，您可能需要從套件安裝到此文件庫系統管理員取得權限。 

#### <a name="file-path-for-in-database-engine-instances"></a>在 Database engine 執行個體的檔案路徑

下表顯示的檔案位置的 R 和 Python 版本和資料庫引擎執行個體組合。 MSSQL13 表示 SQL Server 2016，並且僅限 R。 MSSQL14 指出 SQL Server 2017，並具有 R 和 Python 的資料夾。 

檔案路徑也會包含執行個體名稱。 SQL Server 會安裝[資料庫引擎執行個體](../../database-engine/configure-windows/database-engine-instances-sql-server.md)當做預設執行個體 (MSSQLSERVER) 或使用者定義的具名執行個體。 如果 SQL Server 安裝為具名執行個體，您會看到該名稱，如下所示附加： `MSSQL13.<instance_name>`。

|版本和語言  | 預設路徑|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library|
| 使用 R 的 SQL Server 2017|C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |
| 使用 Python 的 SQL Server 2017 |C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>對獨立伺服器安裝的檔案路徑

下表列出的二進位檔的預設路徑，安裝 SQL Server 2016 R Server （獨立式） 或 SQL Server 2017 Machine Learning Server （獨立式） 伺服器時。 

|Version| 安裝|預設路徑|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning 伺服器，使用 R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning 伺服器，使用 Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果您發現其他具有類似的子資料夾名稱和檔案的資料夾，您可能有的 Microsoft R Server 獨立安裝或[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)。 這類伺服器產品有不同的安裝程式和路徑 （也就是 C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER）。 如需詳細資訊，請參閱[的 Windows 安裝 Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或是[針對 Windows 中安裝 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="next-steps"></a>後續步驟

+ [取得封裝資訊](installed-package-information.md)
+ [安裝新的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [啟用遠端 R 封裝管理](../r/r-package-how-to-enable-or-disable.md)
+ [適用於 R 封裝管理的 RevoScaleR 函式](../r/use-revoscaler-to-manage-r-packages.md)
+ [R 封裝同步處理](../r/package-install-uninstall-and-sync.md)
+ [本機 R 封裝存放庫的 miniCRAN](../r/create-a-local-package-repository-using-minicran.md)
