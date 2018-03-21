---
title: "命令提示字元安裝 SQL Server 機器學習元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2018
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
ms.workload: Inactive
ms.openlocfilehash: c51d8299837f0eda02a07afe1ea4d34d3ecd5e31
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-machine-learning-components-from-the-command-line"></a>從命令列安裝 SQL Server 機器學習服務元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供 intalling SQL Server 機器學習服務元件，從命令列的指示：

+ [在資料庫執行個體](#indb)
+ [將加入至現有的資料庫引擎執行個體](#add-existing)
+ [無訊息安裝](#silent)
+ [獨立伺服器](#shared-feature)

您可以指定安裝程式使用者介面的無訊息、 基本或完整互動。 本文補充[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，涵蓋 R，並將 Python 的機器學習元件特有的參數。

## <a name="pre-install-checklist"></a>預先安裝檢查清單

+ 從提升權限的命令提示字元執行的命令。 

+ 需要資料庫中安裝資料庫引擎執行個體。 您無法安裝只 R 或 Python 的功能，雖然您可以用[以累加方式將它們加入現有的執行個體](#add-existing)。 如果您想只 R，並將 Python 不 database engine，安裝[獨立伺服器](#shared-feature)。

+ 請勿安裝容錯移轉叢集上。 用來隔離 R 和 Python 程序的安全性機制與不相容的 Windows Server 容錯移轉叢集環境。

+ 請勿在網域控制站上安裝。 安裝程式的機器學習服務部分將會失敗。

+ 請避免在同一部電腦上安裝獨立和資料庫中執行個體。 在獨立伺服器將會競用相同的資源，破壞的兩個安裝效能。


## <a name="command-line-arguments"></a>命令列引數

功能引數是必要的因為會授權詞彙合約。 

透過命令提示字元安裝時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援使用 /Q 參數的完整無訊息模式或使用 /QS 參數的簡單無訊息模式。 /QS 參數只會顯示進度、不接受任何輸入，而且不會顯示任何遇到的錯誤訊息。 只有當您指定 /Action=install 時，才支援 /QS 參數。

| 引數 | Description |
|-----------|-------------|
| / 功能 = AdvancedAnalytics | 會安裝在資料庫版本： SQL Server 2017 機器學習服務 （資料庫） 或 SQL Server 2016 R Services （資料庫）。  |
| /FEATURES = SQL_INST_MR | 適用於 SQL Server 2017 只。 與 AdvancedAnalytics 配對。 會安裝 （資料庫） R 功能，包括 Microsoft R Open 與專屬的 R 封裝。 SQL Server 2016 R 服務功能是 R 專用，因此沒有該發行參數。|
| /FEATURES = SQL_INST_MPY | 適用於 SQL Server 2017 只。 與 AdvancedAnalytics 配對。 安裝 Python （資料庫） 功能，包括 Anaconda 和專屬的 Python 封裝。 |
| /FEATURES = SQL_SHARED_MR | 安裝獨立版本的 R 功能： SQL Server 2017 機器學習伺服器 （獨立） 或 SQL Server 2016 R 伺服器 （獨立）。 未繫結至資料庫引擎執行個體的 [共用的功能] 會是獨立伺服器。|
| /FEATURES = SQL_SHARED_MPY | 適用於 SQL Server 2017 只。 安裝單機版的 Python 功能： SQL Server 2017 機器學習伺服器 （獨立）。 未繫結至資料庫引擎執行個體的 [共用的功能] 會是獨立伺服器。|
| /IACCEPTROPENLICENSETERMS  | 表示您接受使用開放原始碼 R 元件授權條款。 |
| / IACCEPTPYTHONLICENSETERMS | 表示您接受授權條款的使用 Python 元件。 |
| /IACCEPTSQLSERVERLICENSETERMS | 表示您接受使用 SQL Server 的授權條款。|
| / MRCACHEDIRECTORY | 離線安裝程式，設定包含 R 元件封包檔的資料夾。 |
| / MPYCACHEDIRECTORY | 離線安裝程式，設定包含 Python 元件封包檔的資料夾。 |


## <a name="indb"></a> 在資料庫執行個體安裝

分析資料庫中可供 database engine 執行個體，加入所需**AdvancedAnalytics**到您安裝的功能。 您可以使用進階分析，安裝資料庫引擎執行個體或[將它加入至現有的執行個體](#add-existing)。 

若要檢視沒有互動式的進度資訊螢幕上的提示，請使用 /qs 引數。

> [!Important]
> 安裝之後，維持兩個額外的設定步驟。 整合不完整，直到執行這些工作。 請參閱[後置安裝工作](#post-install)如需相關指示。

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017： 資料庫引擎，進階分析 Python 和 R

資料庫引擎執行個體並行安裝，提供執行個體名稱和系統管理員 (Windows) 登入。 包含安裝核心和語言元件，以及接受所有的授權條款的功能。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

這個相同的命令，但使用 SQL Server 上的登入資料庫引擎使用混合驗證。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

這個範例只有 Python，顯示您可以藉由略過功能加入一種語言。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016： 資料庫引擎和使用 R 的進階的分析

這個命令與 SQL Server 2017，但是不會 Python 項目，並不是 SQL Server 2016 安裝程式。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> 後續安裝組態 （必要）

套用至資料庫中僅限安裝。

安裝程式完成時，您會有與 R 和 Python、 Microsoft R 和 Python 封裝、 Microsoft R Open、 Anaconda、 工具、 範例和指令碼屬於散發資料庫引擎執行個體。 

完成安裝所需更多的兩個工作：

1. 重新啟動 database engine 服務。

1. 您可以使用此功能之前，請啟用外部指令碼。 請依照下列中的指示[安裝 SQL Server 2017 機器學習服務 （資料庫）](sql-machine-learning-services-windows-install.md)為下一個步驟。 

SQL Server 2016，請改用本文章[安裝 SQL Server 2016 R 服務 （資料庫）](sql-r-services-windows-install.md)。

## <a name="add-existing"></a> 將進階的分析加入現有的資料庫引擎執行個體

當資料庫中的進階的分析加入現有的資料庫引擎執行個體，提供執行個體名稱。 比方說，如果您先前安裝的 SQL Server 2017 資料庫引擎和 Python，您可以使用此命令以新增。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> 無訊息安裝

無訊息安裝隱藏的核取.cab 檔案位置。 基於這個理由，您必須指定要解除封裝 的.cab 檔的位置。 您可以此的暫存目錄。
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> 獨立伺服器安裝

未繫結至資料庫引擎執行個體的 [共用的功能] 會是獨立伺服器。 下列範例會顯示這兩個版本的有效語法。

SQL Server 2017 支援 Python 和 R 獨立伺服器上：

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 是僅限 R:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

安裝程式完成時，您有伺服器、 Microsoft 封裝，R 和 Python，工具，範例和指令碼一部分散發的開放原始碼散發套件。 

若要開啟 R 主控台視窗中，移至 \Program files\Microsoft SQL Server\140 （或 130） \R_SERVER\bin\x64 並按兩下**RGui.exe**。 不熟悉 R 嗎？ 請嘗試此教學課程：[基本 R 命令與 RevoScaleR 函式： 25 的常見範例](https://docs.microsoft.com/en-us/machine-learning-server/r/tutorial-r-to-revoscaler)。

若要開啟 Python 命令，請移至 files\microsoft SQL Server\140\PYTHON_SERVER\bin\x64 並按兩下**python.exe**。

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