---
title: 安裝 SQL Server 2016 R Server （獨立式） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e5457698120536247ad1823b842bb1b8e52b484d
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979280"
---
# <a name="install-sql-server-2016-r-server-standalone"></a>安裝 SQL Server 2016 R Server （獨立式）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何使用 SQL Server 2016 安裝程式來安裝獨立版本**SQL Server 2016 R Server**。

## <a name="bkmk_prereqs"> </a> 預先安裝檢查清單

需要 SQL Server 2016。 如果您有 SQL Server 2017，請安裝[SQL Server 2017 Machine Learning Server （獨立式）](sql-machine-learning-standalone-windows-install.md)改。

如果您安裝任何舊版的 Revolution Analytics 工具或套件，您必須先解除。 

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2016 安裝精靈。 我們建議您安裝 Service Pack 1 或更新版本。

2. 在 **安裝**索引標籤上，按一下**新的 R Server （獨立式） 安裝**。
    
     ![啟動的 R Server （獨立式） 安裝程式](media/2016-setup-installation-rsvr.png "啟動的 R Server （獨立式） 安裝程式")
    
3.  在 [功能選擇]  頁面上，應該已經選取下列選項：
    
    **R Server (獨立式)**  
    
    ![功能的 R Server （獨立式） 的選項](media/2016setup-rserver-features.png "功能選項的 R Server （獨立式）")
    
    您可以忽略所有其他選項。 
    
    > [!NOTE]
    > 避免安裝**共用功能**如果您執行安裝程式的電腦上其中 R Services 已安裝的 SQL Server 資料庫內分析。 這會建立重複的程式庫。
    > 
    > SQL Server 中執行的 R 指令碼來為未與其他 database engine 服務所使用的記憶體相衝突的 SQL Server 所管理，而獨立 R 伺服器沒有這類條件約束，並可能會干擾其他資料庫作業。
    > 
    > 我們通常建議您安裝 R Server （獨立式） 不同的電腦上從 SQL Server R Services （資料庫）。

4.  接受授權條款，下載並安裝 Microsoft R Open。 無法使用 [接受]  按鈕時，您可以按一下 [下一步] 。
    
    這些元件，以及它們所需要的任何必要條件的安裝可能需要一段時間。
    
5.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝] 。

## <a name="default-installation-folders"></a>預設安裝資料夾

當您安裝 R 伺服器使用 SQL Server 安裝程式時，R 程式庫會安裝在與您用於安裝的 SQL Server 版本相關聯的資料夾中。 在此資料夾中，您也可以找到範例資料、 R 基底套件的文件和文件的 R 工具和執行階段。

不過，如果您安裝 Microsoft R 伺服器使用個別的 Windows 安裝程式 （不 SQL 安裝程式），或如果您升級使用不同的 Windows installer，R 程式庫會安裝在不同的資料夾中。

雖然我們建議您不要它，您也在相同電腦上安裝 SQL Server 與 R Services （資料庫） 的執行個體，R 程式庫和工具的第二個複本會安裝在不同的資料夾中。

下表列出每個安裝的路徑。

|版本| 安裝方法 | 預設資料夾|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 安裝精靈|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Windows 的獨立安裝程式|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning 伺服器 (獨立式) |  SQL Server 2017 安裝精靈中，使用 R 語言選項 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning 伺服器 (獨立式) |  SQL Server 2017 安裝精靈中，使用 Python 語言選項 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Machine Learning 伺服器 (獨立式) |  Windows 的獨立安裝程式 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (資料庫內) |SQL Server 2016 安裝精靈|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning 服務 (資料庫內) |SQL Server 2017 安裝精靈中，使用 R 語言選項|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Machine Learning 服務 (資料庫內) |SQL Server 2017 安裝精靈中，使用 Python 語言選項| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

## <a name="development-tools"></a>開發工具

開發 IDE 不會安裝成在安裝程序。 不需要額外的工具，當所有的標準工具都隨附，就會提供使用 R 或 Python 的散發套件。

建議您試用新版[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或是[適用於 Visual Studio 的 Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio)。 Visual Studio 支援同時 R 和 Python，以及資料庫開發工具與 SQL Server 的連線能力和 BI 工具。 不過，您可以使用任何慣用的開發環境，包括 RStudio。
  
## <a name="get-help"></a>取得說明

需要安裝或升級的說明嗎？ 如需常見問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查的執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續的步驟

R 開發人員可以開始使用一些簡單的範例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程： 在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。
+ [適用於 R 開發人員教學課程： 在資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要檢視機器學習服務依據真實世界案例的範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。

