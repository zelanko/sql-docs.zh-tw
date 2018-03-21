---
title: "安裝 SQL Server 2016 R Server （獨立） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 48f28b7a8d357e80e7defb6d6a8d446041380fbf
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2016-r-server-standalone"></a>安裝 SQL Server 2016 R Server （獨立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章描述如何使用 SQL Server 2016 安裝程式安裝單機版**SQL Server 2016 R 伺服器**。 如果您有 Enterprise Edition 或軟體保證，實際執行伺服器上安裝獨立 R 伺服器是免費的。

## <a name="bkmk_prereqs"> </a> 預先安裝檢查清單

需要 SQL Server 2016。 如果您有 SQL Server 2017，請安裝[SQL Server 2017 機器學習伺服器 （獨立）](sql-machine-learning-standalone-windows-install.md)改為。

如果您安裝任何舊版的 Revolution Analytics 工具或封裝，您必須先解除。 

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  

## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動 SQL Server 2016 安裝程式精靈。 我們建議您安裝 Service Pack 1 或更新版本。

2. 在**安裝**索引標籤上，按一下 **安裝新的 R 伺服器 （獨立）**。
    
     ![開始安裝 R Server 的獨立](media/2016-setup-installation-rsvr.png "啟動 R Server 的獨立安裝程式")
    
3.  在 [功能選擇]  頁面上，應該已經選取下列選項：
    
    **R Server (獨立式)**  
    
    ![功能選項的 R 伺服器獨立](media/2016setup-rserver-features.png "功能 R 伺服器獨立的選項")
    
    您可以忽略所有其他選項。 
    
    > [!NOTE]
    > 避免安裝**共用功能**如果您執行安裝程式的電腦上其中 R 服務已安裝的 SQL Server 資料庫中的分析。 這會建立重複的程式庫。
    > 
    > SQL Server 中執行 R 指令碼由 SQL Server，來為未與其他 database engine 服務所使用的記憶體衝突管理，而獨立 R 伺服器沒有這類條件約束，並可能會干擾其他資料庫作業。
    > 
    > 我們通常會建議您安裝 R Server （獨立） 另一部電腦上從 SQL Server R Services （資料庫）。

4.  接受授權條款，下載並安裝 Microsoft R Open。 無法使用 [接受]  按鈕時，您可以按一下 [下一步] 。
    
    這些元件和它們所需要的任何必要條件的安裝可能需要一點時間。
    
5.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝] 。

## <a name="default-installation-folders"></a>預設安裝資料夾

當您安裝 R Server 使用 SQL Server 安裝程式時，R 程式庫會安裝在與您用於安裝的 SQL Server 版本相關聯的資料夾。 在這個資料夾中，您也可以找到範例資料、 R 基底套件，文件及文件的 R 工具和執行階段。

不過，如果您安裝 Microsoft R Server 使用不同的 Windows installer （不 SQL 安裝程式），或您升級使用個別的 Windows installer，R 程式庫會安裝在不同的資料夾。

雖然我們建議您不要它，如果您同時在相同電腦上安裝與 R Services （資料庫） 的 SQL Server 執行個體，第二個副本 R 程式庫和工具會安裝在不同的資料夾。

下表列出每個安裝的路徑。

|版本| 安裝方法 | 預設資料夾|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 安裝程式精靈|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Windows 的獨立安裝程式|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning 伺服器 (獨立式) |  SQL Server 2017 安裝精靈中，與 R 語言選項 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning 伺服器 (獨立式) |  SQL Server 2017 安裝精靈中，使用 Python 語言選項 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Machine Learning 伺服器 (獨立式) |  Windows 的獨立安裝程式 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (資料庫內) |SQL Server 2016 安裝程式精靈|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning 服務 (資料庫內) |SQL Server 2017 安裝精靈中，與 R 語言選項|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Machine Learning 服務 (資料庫內) |SQL Server 2017 安裝精靈中，使用 Python 語言選項| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

## <a name="development-tools"></a>開發工具

開發 IDE 不會安裝成在安裝程序。 不需要額外的工具，包含所有的標準工具時，就會提供與 R 或 Python 的分佈。

我們建議您嘗試為新版本的[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或[for Visual Studio 的 Python](https://docs.microsoft.com/en-us/visualstudio/python/installing-python-support-in-visual-studio)。 Visual Studio 支援同時 R 和 Python，以及資料庫開發工具與 SQL Server 的連線與 BI 工具。 不過，您可以使用任何慣用的開發環境，包括 RStudio。
  
## <a name="get-help"></a>取得說明

需要協助以安裝或升級嗎？ 常見的問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-機器學習服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續的步驟

R 開發人員可以開始使用一些簡單的案例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程： 在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。
+ [R 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要檢視的機器學習，根據真實世界案例的範例，請參閱[機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)。

