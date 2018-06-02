---
title: 安裝 SQL Server 2017 機器學習伺服器 （獨立） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cb906a8a05221204ec10310d652f6891861d35e2
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "34708266"
---
# <a name="install-sql-server-2017-machine-learning-server-standalone-on-windows"></a>安裝 SQL Server 2017 機器學習 Windows 上的伺服器 （獨立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安裝程式包含安裝的機器學習 SQL Server 外部執行的伺服器的選項。 這個選項可能會很有用，如果您需要開發高效能的機器學習解決方案，可以使用遠端計算內容，交換切換本機伺服器和遠端機器學習伺服器上的 Spark 叢集，或另一個 SQL Server 上執行個體。
  
這篇文章描述如何使用 SQL Server 安裝程式安裝單機版**SQL Server 2017 機器學習伺服器**。 

## <a name="bkmk_prereqs"> </a> 預先安裝檢查清單

需要 SQL Server 2017。 如果您有 SQL Server 2016，請安裝[SQL Server 2016 R 伺服器 （獨立）](sql-r-standalone-windows-install.md)改為。

如果您已安裝舊版，例如 SQL Server 2016 R 伺服器 （獨立） 或 Microsoft R Server，解除安裝現有的安裝之後才能繼續。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2017 的安裝精靈。

2. 按一下**安裝**索引標籤，然後選取**安裝新的機器學習伺服器 （獨立）**。
    
     ![機器學習 Server 獨立安裝](media/2017setup-installation-page-mlsvr.png "啟動的機器學習 Server 獨立安裝")

3. 規則檢查完成之後，接受 SQL Server 授權條款，並選取新的安裝。

4. 在**特徵選取**頁面上，下列選項應該已經選取：

    - Microsoft 的機器學習伺服器 （獨立）

    - R 和 Python 兩者預設會選取。 您可以取消選取其中一個語言，但我們建議您安裝至少其中一個支援的語言。

     ![機器學習 Server 獨立安裝](media/2017setup-features-page-mlsvr-rpy.png "啟動的機器學習 Server 獨立安裝")
    
    您應該忽略所有其他選項。 
    
    > [!NOTE]
    > 避免安裝**共用功能**如果電腦已安裝的 SQL Server 資料庫中的分析機器學習服務。 這會建立重複的程式庫。
    > 
    > 此外，SQL Server 中執行的 R 或 Python 指令碼由 SQL Server，來為未與其他 database engine 服務所使用的記憶體衝突管理，而獨立機器學習伺服器沒有這類條件約束，並可能會干擾其他資料庫作業. 最後，資料庫管理員通常會封鎖透過 RDP 工作階段，通常會使用實施，遠端存取。
    > 
    > 基於這些理由，我們通常會建議您在 SQL Server 機器學習服務從另一部電腦上安裝機器學習伺服器 （獨立）。

5.  接受授權條款，下載並安裝的機器學習服務元件。 如果您安裝這兩種語言，個別的授權合約是 Microsoft R 和 Python 需要。
    
     ![Python 授權合約](media/2017setup-python-license.png "Python 授權合約")
    
    這些元件和它們所需要的任何必要條件的安裝可能需要一點時間。 無法使用 [接受]  按鈕時，您可以按一下 [下一步] 。

6.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝] 。

### <a name="default-installation-folders"></a>預設安裝資料夾

當您安裝 R 伺服器或使用 SQL Server 安裝程式的機器學習伺服器，R 程式庫會安裝在與您用於安裝的 SQL Server 版本相關聯的資料夾。 在這個資料夾中，您也可以找到範例資料、 R 基底套件，文件及文件的 R 工具和執行階段。

不過，如果您使用不同的 Windows installer，安裝或升級使用個別的 Windows installer，R 程式庫會安裝在不同的資料夾。

只供參考，如果您已安裝的 SQL Server 執行個體與 R Services （資料庫） 或機器學習服務 （資料庫），且該執行個體在相同的電腦上的 R 程式庫和工具預設會安裝在不同的資料夾。

下表列出每個安裝的路徑。

|版本| 安裝方法 | 預設資料夾|
|----|----|----|
|SQL Server 2017 機器學習伺服器 （獨立） |  SQL Server 2017 安裝精靈 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft 的機器學習伺服器 （獨立） |  Windows 的獨立安裝程式 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 機器學習服務 （資料庫） |SQL Server 2017 安裝精靈中，與 R 語言選項|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R 伺服器 （獨立） |  SQL Server 2016 安裝程式精靈 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R 服務 （資料庫） |SQL Server 2016 安裝程式精靈|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

## <a name="development-tools"></a>開發工具

開發 IDE 不會安裝成在安裝程序。 不需要額外的工具，包含所有的標準工具時，就會提供與 R 或 Python 的分佈。

我們建議您嘗試為新版本的[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或[for Visual Studio 的 Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio)。 Visual Studio 支援同時 R 和 Python，以及資料庫開發工具與 SQL Server 的連線與 BI 工具。 不過，您可以使用任何慣用的開發環境，包括 RStudio。

## <a name="get-help"></a>取得說明

需要協助以安裝或升級嗎？ 常見的問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-機器學習服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續的步驟

R 開發人員可以開始使用一些簡單的案例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程： 在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以瞭解如何使用 SQL Server 中的 Python，依照這些教學課程：

+ [教學課程： 在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [Python 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視的機器學習，根據真實世界案例的範例，請參閱[機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)。
