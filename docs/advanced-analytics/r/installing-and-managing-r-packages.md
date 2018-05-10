---
title: 預設 SQL Server R 和 SQL Server 機器學習中的 R，並將 Python 封裝程式庫 |Microsoft 文件
description: SQL Server R 服務，R Server 機器學習服務 （資料庫），與機器學習伺服器 （獨立） 所安裝的 R，並將 Python 封裝
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ee2c8124cf3487ca300c0b08ea113c8e66b114f4
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="default-r-and-python-packages-in-sql-server"></a>在 SQL Server 中的預設 R，並將 Python 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文涵蓋封裝程式庫、 位置和 SQL server 安裝的 R，並將 Python 封裝版本。 

## <a name="using-the-default-instance-library"></a>使用預設執行個體文件庫

當您安裝 SQL server 的機器學習服務時，在您安裝的每種語言的執行個體層級建立單一封裝程式庫。 

所有的指令碼或程式碼，執行中的 SQL Server 上資料庫必須從執行個體文件庫載入函式。 SQL Server 無法存取封裝安裝到其他文件庫。 這適用於遠端的用戶端。 從遠端用戶端連線到伺服器，當您想要 server 計算內容中執行任何 R 或 Python 程式碼只能使用安裝執行個體文件庫中的封裝。

若要保護伺服器資產，預設執行個體的程式庫會安裝到受保護的資料夾已向 SQL Server，而且可以只由電腦管理員修改。 如果您不是電腦的擁有者，您可能需要從系統管理員才能安裝封裝至這個文件庫中取得的權限。 

即使您擁有電腦時，您應該先將封裝新增至執行個體文件庫來考慮任何特定的 R 或 Python 封裝在伺服器環境的實用性。 請考慮因素，例如大小的封裝檔案，並且需要進行多個版本，以及封裝是否需要網路或網際網路存取。

### <a name="in-database-engine-instance-file-paths"></a>在 Database engine 執行個體的檔案路徑

下表顯示的檔案位置的 R，並將 Python 版本和資料庫引擎執行個體組合。 

|版本 | 執行個體名稱|預設路徑|
|--------|--------------|------------|
| SQL Server 2016 |預設執行個體| C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library|
| SQL Server 2016 |具名執行個體 (named instance) | C:\Program Files\Microsoft SQL Server\MSSQL13。 < instance_name > \R_SERVICES\library|
| R 與 SQL Server 2017|預設執行個體 | C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library |
| R 與 SQL Server 2017|具名執行個體 (named instance)| C:\Program Files\Microsoft SQL Server\MSSQL14。MyNamedInstance\R_SERVICES\library |
| SQL Server 2017 使用 Python |預設執行個體 | C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\library |
| SQL Server 2017 使用 Python|具名執行個體 (named instance)| C:\Program Files\Microsoft SQL Server\MSSQL14。 < instance_name > \PYTHON_SERVICES\library |

### <a name="standalone-server-file-paths"></a>獨立伺服器的檔案路徑 

安裝 SQL Server 2016 R 伺服器 （獨立） 或 SQL Server 2017 機器學習伺服器 （獨立） 伺服器時下, 表列出的二進位檔的預設路徑。 

|版本| 安裝|預設路徑|
|------|------|------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|機器學習服務伺服器，以 R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|機器學習服務伺服器，使用 Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果您發現有類似的子資料夾名稱和檔案的其他資料夾，您可能會有 Microsoft R Server 的獨立安裝或[Machine Learning 伺服器](https://docs.microsoft.com/machine-learning-server/)。 這些伺服器產品有不同的安裝程式與路徑 （也就是 C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER）。 如需詳細資訊，請參閱[安裝機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或[適用於 Windows 安裝 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="what-is-included-in-a-default-installation"></a>在預設安裝中包含的內容

本章節摘要說明包含在預設安裝的 R，並將 Python 功能。

### <a name="r-components"></a>R 元件

元件包括 Microsoft 的開放原始碼 R 為分佈[Microsoft R Open](https://mran.microsoft.com/open)。 基底 R 封裝包括核心功能，例如**stats**和**utils**。 您可以執行`installed.packages(priority = "base")`傳回封裝清單。 R 的基底安裝也包含許多的範例資料集，以及標準的 R 工具，例如 RGui （輕量型互動式編輯器） 和 RTerm （R 命令提示字元）。

Microsoft 封裝包含[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)遠端計算內容資料流中，平行資料匯入和轉換 rx 函數的執行，如模型、 視覺化和分析。 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)新增機器學習模型其他封裝包含[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)在 R 中撰寫 MDX 陳述式和[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)在預存程序中包含 R 指令碼。


|版本             | R 版本       | Microsoft 封裝    |
|--------------------|-----------------|-----------------------|
| SQL Server 2016 R Services | 3.2.2   | RevoScaleR sqlrutil  |
| SQL Server 2017 Machine Learning 服務| 3.4.3 | RevoScaleR，MicrosoftML，olapR sqlrutil|

您可以將封裝和預先安裝的模型加入 SQL Server 2016 R 服務的現代的生命週期支援原則的繫結。 繫結變更服務模型。 根據預設，初始安裝之後，R 封裝會重新整理透過 service pack 和累計更新。 其他封裝及核心 R 元件的完整版本升級僅能透過產品升級 （從 SQL Server 2016 到 SQL Server 2017) 或透過繫結 R 支援 Microsoft 機器學習服務伺服器。 如需詳細資訊，請參閱[中 SQL Server 升級 R 和 Python 元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="python-components"></a>Python 元件

SQL Server 2017 加入 Python 元件。 當您選取的 Python 語言選項時，會安裝 Anaconda 發佈。 除了 Python 程式碼程式庫，標準安裝包含範例資料、 單元測試及範例指令碼。 

Microsoft 封裝包含[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Python 的對等 RevoScaleR，與資料流，為的平行執行的資料匯入和轉換、 模型、 視覺化和分析的接收函式。 其他的 Python 封裝是[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)訓練和轉換、 計分、 文字和影像分析和擷取特徵的值衍生自現有資料。

SQL Server 2017 機器學習為 R 和 Python 支援第一次的釋放。

|版本             | Anaconda 版本| Microsoft 封裝    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning 服務  | 4.2 透過 Python 3.5 | revoscalepy microsoftml |

初始安裝之後，Python 封裝會重新整理透過 service pack 和累計更新，但完整的版本升級時，才可以透過繫結至 Microsoft Machine Learning 伺服器的 Python 支援。 如需詳細資訊，請參閱[中 SQL Server 升級 R 和 Python 元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="administrative-permissions-for-package-installation"></a>封裝安裝的系統管理權限

封裝安裝所需的權限已變更 SQL Server 2016 和 SQL Server 2017 之間。

+ 在 SQL Server 2016 中，系統管理存取權，才能安裝新的 R 封裝。
+ 在 SQL Server 2017，系統管理員身分安裝封裝，R 和 Python，您可以繼續，這可能是最簡單的方法。 

    DDL 陳述式，建立外部程式庫可讓資料庫管理員，而不使用的 R 工具安裝封裝。 

    如果您使用的封裝管理功能的機器學習伺服器時，您可以使用 RevoScaleR 安裝 R 封裝，在資料庫層級。 資料庫管理員必須啟用功能，並再授與使用者的能力是根據每個資料庫來安裝自己的封裝。 如需詳細資訊，請參閱[啟用封裝管理使用 Ddl](r-package-how-to-enable-or-disable.md)。

### <a name="user-libraries-are-not-supported"></a>不支援使用者文件庫

使用者無法安裝封裝到安全的位置通常求助於安裝套件使用者程式庫。 不過，這是不可能在 SQL Server 環境中。 通常限制檔案系統存取的伺服器上，而且即使您擁有系統管理員權限及存取伺服器上的使用者文件資料夾時，執行 SQL Server 中的外部指令碼執行階段無法存取安裝預設執行個體外部的任何封裝程式庫。 不過，因應措施可能會有。 如需有關如何解決問題的相關使用者程式庫的秘訣，請參閱[R 使用者程式庫的因應措施](packages-installed-in-user-libraries.md)。

## <a name="next-steps"></a>後續的步驟

+ [取得封裝資訊](determine-which-packages-are-installed-on-sql-server.md)
+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [啟用 R 封裝的遠端管理](r-package-how-to-enable-or-disable.md)
+ [RevoScaleR 函數的 R 封裝管理](use-revoscaler-to-manage-r-packages.md)
+ [R 封裝的同步處理](package-install-uninstall-and-sync.md)
+ [本機的 R 封裝儲存機制的 miniCRAN](create-a-local-package-repository-using-minicran.md)
