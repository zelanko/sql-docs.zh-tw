---
title: 預設的 SQL Server 上的機器學習服務封裝程式庫 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 64b085c2314e4c97694e91924cb15d43315143e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="default-package-libraries-for-machine-learning-on-sql-server"></a>預設 SQL Server 上的機器學習服務封裝程式的庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章描述 R，並將 Python 與 SQL Server 一起安裝的預設程式庫。 本文提供的預設位置，這些文件庫，並說明如何判斷哪些封裝和 R 的版本或 Python 安裝每個執行個體文件庫中。

## <a name="using-the-default-instance-library"></a>使用預設執行個體文件庫

當您安裝 SQL server 的機器學習服務時，在您安裝的每種語言的執行個體層級建立單一封裝程式庫。 SQL Server 無法存取封裝安裝到其他文件庫。

如果您從遠端用戶端連線到伺服器，您想要 server 計算內容中執行任何 R 或 Python 程式碼可以使用安裝在執行個體文件庫中的封裝。

若要保護伺服器資產，預設執行個體的程式庫會安裝到受保護的資料夾已向 SQL Server，而且可以只由電腦管理員修改。 如果您不是電腦的擁有者，您可能需要從系統管理員才能安裝封裝至這個文件庫中取得的權限。 

即使您擁有電腦時，您應該先將封裝新增至執行個體文件庫來考慮任何特定的 R 或 Python 封裝在伺服器環境的實用性。 請考慮因素，例如大小的封裝檔案，並且需要進行多個版本，以及封裝是否需要網路或網際網路存取。

### <a name="sql-server"></a>SQL Server

|版本 | 執行個體名稱|預設路徑|
|------|------|------|
| SQL Server 2016 |預設執行個體|`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`|
| SQL Server 2016 |具名執行個體 (named instance) |`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES\library`|
| R 與 SQL Server 2017|預設執行個體 |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` |
| R 與 SQL Server 2017|具名執行個體 (named instance)|`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` |
| SQL Server 2017 使用 Python |預設執行個體 |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library` |
| SQL Server 2017 使用 Python|具名執行個體 (named instance)|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES\library` |

### <a name="r-server-standalone-or-machine-learning-server-standalone"></a>R 伺服器 （獨立） 或機器學習伺服器 （獨立）

獨立伺服器安裝使用 SQL Server 安裝程式時下, 表列出的二進位檔的預設路徑。 

|版本| 安裝|預設路徑|
|------|------|------|
| SQL Server 2016|R Server (Standalone)| |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|機器學習服務伺服器，以 R |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|機器學習服務伺服器，使用 Python |`C:\Program Files\Microsoft SQL Server\130\PYTHON_SERVER`|

如果您安裝 Microsoft R 伺服器或使用不同的 Windows installer 的機器學習伺服器時，預設路徑會不同： 通常，就像`C:\Program Files\Microsoft\R Server\R_SERVER`。 如需詳細資訊，請參閱：
 
+ [安裝機器學習適用於 Windows 的伺服器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安裝 R Server 9.1 適用於 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="what-is-included-in-a-default-installation"></a>在預設安裝中包含的內容

本章節提供預設安裝的 R 或 Python 功能的摘要。

### <a name="default-r-installation-for-sql-server"></a>SQL Server 的預設 R 安裝

根據預設 R**基底**已安裝的套件。 基底套件包含這類封裝所提供的核心功能`stats`和`utils`。

R 的基底安裝也包含許多的範例資料集，以及標準的 R 工具，例如 RGui （輕量型互動式編輯器） 和 RTerm （R 命令提示字元）。

SQL Server 2016 中 SQL Server 2017 R 的安裝也包含**RevoScaleR**封裝，相關的增強的封裝和提供者，可支援遠端計算內容資料流中，平行執行 rx 函式，並許多其他功能。

若要升級的 RevoScaleR 封裝，請使用繫結來升級機器學習服務元件，或修補或升級至較新版的 SQL Server 執行個體。

+ 如需增強的 R 功能的概觀，請參閱[需機器學習伺服器](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ 若要下載到用戶端電腦上的 RevoScaleR 程式庫，安裝[Microsoft R 用戶端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

### <a name="default-python-installation-for-sql-server"></a>預設 SQL Server 的 Python 安裝

如果您選取的機器學習功能和 Python 語言選項時，會安裝 Anaconda 發佈。 確切的版本取決於您已安裝的 SQL Server 的版本，不論您已升級使用機器學習 Server 安裝程式的執行個體。

|版本| Anaconda 版本| 其他變更|
|------|------|------|
| SQL Server 2017 RTM| 3.5.2| 新： revoscalepy|
| 透過機器學習伺服器 9.2.1 2017 年 9 月的更新| Anaconda 4.2| revoscalepy 的更新 |
| SQL Server 2017 CU3| Anaconda 4.2| revoscalepy 的更新 |

除了 Python 程式碼程式庫，標準安裝包含範例資料、 單元測試及範例指令碼。

## <a name="restrictions-and-known-issues"></a>限制與已知的問題

執行 SQL Server 中的任何解決方案可以使用**只**安裝在執行個體相關聯的預設程式庫中的封裝。

如果您使用繫結來升級執行個體中的 R 元件，可以變更執行個體文件庫的路徑。 請務必確認由 SQL Server 目前使用的程式庫的路徑。

## <a name="administrative-permissions-required-for-package-installation"></a>封裝安裝所需的系統管理權限

封裝安裝所需的權限已變更 SQL Server 2016 和 SQL Server 2017 之間。

+ 在 SQL Server 2016 中，系統管理存取權，才能安裝新的 R 封裝。

+ 在 SQL Server 2017，系統管理員身分安裝封裝，R 和 Python，您可以繼續，這可能是最簡單的方法。

    DDL 陳述式，建立外部程式庫可讓資料庫管理員，而不使用的 R 工具安裝封裝。 

    如果您使用的封裝管理功能的機器學習伺服器時，您可以使用 RevoScaleR 安裝 R 封裝，在資料庫層級。 資料庫管理員必須啟用功能，並再授與使用者的能力是根據每個資料庫來安裝自己的封裝。 如需詳細資訊，請參閱[啟用封裝管理使用 Ddl](r-package-how-to-enable-or-disable.md)。

### <a name="user-libraries-are-not-supported"></a>不支援使用者文件庫

使用者無法安裝封裝到安全的位置通常求助於安裝套件使用者程式庫。 不過，這是不可能在 SQL Server 環境中。即使檔案系統存取權通常會在伺服器上限制。

即使您擁有系統管理員權限及存取伺服器上的使用者文件資料夾時，執行 SQL Server 中的外部指令碼執行階段無法存取安裝預設執行個體文件庫之外的任何封裝。

如需有關如何解決問題的相關使用者程式庫的秘訣，請參閱[封裝安裝在使用者程式庫](packages-installed-in-user-libraries.md)。