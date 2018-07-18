---
title: 什麼是 SQL Server 機器學習服務？ | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ecd58ee9670724a2732ce8aabc5d9f2c62042995
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585450"
---
# <a name="what-is-sql-server-machine-learning-services"></a>什麼是 SQL Server 機器學習服務？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 機器學習服務是內嵌、 預測分析和資料科學引擎，為預存程序、 T-SQL 指令碼包含 R 或 Python 陳述式，或做為 R 或 Python 程式碼，其中包含可執行 SQL Server 資料庫中的 R，並將 Python 程式碼T-SQL。 

機器學習服務的索引鍵的價值主張是其專屬的套件的能力，提供進階的分析，在小數位數，並且能夠讓計算和處理資料所在的位置，因而不須透過提取資料網路。

有兩個 SQL Server 中使用機器學習功能的選項： 

+ [**SQL Server 機器學習服務 （資料庫）** ](r/sql-server-r-services.md) database engine 執行個體，計算引擎完全整合與 database engine 中運作。 大部分安裝都將此選項。
+ [**SQL Server 機器學習伺服器 （獨立）** ](r/r-server-standalone.md)是機器學習 Server for Windows 的執行與 database engine 無關。 雖然您可以使用 SQL Server 安裝程式來安裝伺服器，此功能不是執行個體感知的。 在功能上，它相當於非 SQL-Server [Microsoft 機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

## <a name="r-and-python-packages"></a>R 和 Python 封裝

每個語言的支援是透過用來建立及定型模型的計分資料，以及使用基礎的系統資源的平行處理的各種類型的專屬 Microsoft 套件。

因為專屬的封裝會建立開放原始碼 R，並將 Python 發佈，指令碼或您在 SQL Server 中執行的程式碼可以同時也呼叫基底函式，並使用與 SQL Server 中提供的語言版本相容的第三方封裝 (Python 3.5 和最新版本的 R，目前 3.3.3）。

| R  | Python | 描述 |
|-----------|----------------|-------------|
| [RevoScaleR](r/revoscaler-overview.md) | [revoscalepy](python/what-is-revoscalepy.md)   | 這些程式庫中的函式是最常使用。 這些程式庫中找到資料轉換和操作、 統計摘要、 視覺化和模型化和分析的許多種。 此外，這些程式庫中的函式自動工作負載分散到可用的核心進行平行處理，在協調，並計算引擎所管理的資料區塊上運作的能力。 |
| [MicrosoftML](using-the-microsoftml-package.md) | [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 領先業界的機器學習演算法的映像功能，其潛在、 分類問題，以及更多。 |
| [olapR](r/how-to-create-mdx-queries-using-olapr.md) | 無 | 建置或執行 R 指令碼中的 MDX 查詢。
| [sqlRUtils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) | 無 | 讓 T-SQL 的 R 指令碼的函式預存程序，預存程序註冊資料庫，並從 R 開發環境中執行預存程序。
| [mrsdeploy](operationalization-with-mrsdeploy.md) | 無 | 主要是用在非 SQL 安裝的機器學習 Server，例如[（獨立） 版本](r/r-server-standalone.md)。 使用此封裝來部署和裝載 web 服務、 建立向外延展拓撲與專用的 web 和計算節點、 本機和遠端工作階段，執行診斷，以及其他的之間切換。 （資料庫） 安裝，請使用此套件中用戶端容量： 例如，若要存取遠端伺服器上的 web 服務專用於執行只機器學習服務工作負載。 |

自訂 R，並將 Python 程式碼的可攜性是透過套件發佈和多項產品內建解譯器來定址。 隨附於 SQL Server 相同的封裝也會提供數個其他 Microsoft 產品和服務，包括呼叫非 SQL 版本中[Microsoft Machine Learning 伺服器](https://docs.microsoft.com/machine-learning-server/)。 可用的用戶端，包括我們的 R，並將 Python 解譯器包括[Microsoft R 用戶端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)和[Python 程式庫](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)。

封裝和解譯器也會提供數項[Azure 虛擬機器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux)，Azure Machine Learning 中，與 Azure 的服務，像是[HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight)。 


## <a name="use-cases"></a>使用案例

**資料庫分析**

開發人員和分析師通常具有本機 SQL Server 執行個體上執行的程式碼。 如果您有 SQL Server 和 IDE 例如[Visual Studio 以 R](https://docs.microsoft.com/visualstudio/rtvs/)或[Visual Studio 使用 Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio)的相同電腦上，建置、 定型和測試模型在本機中任一語言。 本機存取可簡化管理套件： 身為系統管理員，您可以載入其他第三方封裝，該角色中使用內建權限。

分析資料庫中的最常見的方法是使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)執行 R 或 Python 指令碼。 教學課程中所列[後續步驟](#next-steps)可協助您開始。

**用戶端-伺服器組態**

有一個 IDE 任何用戶端工作站，從安裝[Microsoft R 用戶端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)或[Python 程式庫](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)，然後撰寫推入執行的程式碼 (稱為*遠端計算內容*)資料和遠端的 SQL Server 的作業。 

同樣地，如果您使用 Developer edition，您可以建立使用相同的程式庫和解譯器，用戶端工作站上的方案，然後再部署 SQL Server 機器學習服務 （資料庫） 上的實際執行程式碼。 

## <a name="version-history"></a>版本歷程記錄

SQL Server 2017 機器學習服務是新一代的 SQL Server 2016 R 服務，加強可包含 Python。 下表是從開始到目前的版本中的所有版本的完整清單。 

| 產品名稱 | 引擎版本 | 發行日期 |
|--------------|---------|--------------|
| SQL Server 2017 機器學習服務 （資料庫） | R 伺服器 9.2.1 <br/> Python Server 9.2 | 2017 年 10 月 |
| SQL Server 2017 機器學習伺服器 （獨立） | R 伺服器 9.2.1 <br/> Python Server 9.2 | 2017 年 10 月 |
| SQL Server 2016 R 服務 （資料庫） | R 伺服器 9.1  | 2017 年 7 月  |
| SQL Server 2016 R 伺服器 （獨立）  |  R 伺服器 9.1 | 2017 年 7 月 |



## <a name="documentation-for-each-version"></a>每個版本的文件

SQL Server 文件的最新版本與版本無關。 SQL Server 機器學習服務 Python 才可用在 2017年和更新版本，在所有版本中支援 R 時。 除非另有說明否則您可以假設 R 文件適用於 2016年和 2017年版本。


## <a name="related-machine-learning-products"></a>相關的機器學習的產品

 +  [佈建 Azure 虛擬機器](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure marketplace 包括包括機器學習 Server 或 R Server 的多個虛擬機器映像。 在 Microsoft Azure 中建立虛擬機器是最快速的方式來開發和部署的預測模型。 映像隨附於調整及共用已設定，使其更容易內嵌應用程式內的分析，以及與後端系統整合的功能。

+ [資料科學虛擬機器](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)

  資料科學虛擬機器的最新版本包括機器學習伺服器、 SQL Server，加上最受歡迎的機器學習工具陣列所有預先安裝，並測試。 建立 Jupyter 筆記本，來開發方案 Julia，並使用如 MXNet、 CNTK，以及 TensorFlow GPU 啟用深入學習程式庫。

<a name="next-steps"></a>

## <a name="next-steps"></a>後續的步驟

**步驟 1:** 安裝及設定軟體。 

+ [安裝 SQL Server 2017 機器學習服務 （資料庫）](install/sql-machine-learning-services-windows-install.md)

**步驟 2:** 開始使用這些教學課程的其中一個程式碼使用：

+ [教學課程： 在 T-SQL 中執行 Python](tutorials/run-python-using-t-sql.md)
+ [教學課程： 在 T-SQL 中執行 R](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

**步驟 3:** 加入您最愛的 R，並將 Python 封裝，並使用它們，以及 Microsoft 所提供的封裝

+ [SQL Server 的 R 封裝管理](r/install-additional-r-packages-on-sql-server.md)
