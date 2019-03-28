---
title: 命令提示字元安裝 R 和 Python 元件-SQL Server Machine Learning
description: 執行 SQL Server 命令列安裝，以加入 SQL Server 資料庫引擎執行個體上的 R 語言和 Python 整合。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: d852cc745578d852b2c8235ebcaf3614020a1bb8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511745"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>安裝 SQL Server machine learning R 和 Python 的元件，從命令列
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章提供 intalling SQL Server 機器學習服務元件，從命令列的指示：

+ [在資料庫的新執行個體](#indb)
+ [將新增至現有的資料庫引擎執行個體](#add-existing)
+ [無訊息安裝](#silent)
+ [新的獨立伺服器](#shared-feature)

您可以指定安裝程式使用者介面的無訊息、 基本或完整互動。 本文補充[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，涵蓋 R 和 Python 機器學習服務元件的唯一參數。

## <a name="pre-install-checklist"></a>預先安裝檢查清單

+ 從提升權限的命令提示字元執行的命令。 

+ 需要資料庫中安裝資料庫引擎執行個體。 您無法安裝只是 R 或 Python 的功能，雖然您可以[將它們以累加方式新增至現有的執行個體](#add-existing)。 如果您想只是 R 和 Python，而不需要 database engine，安裝[獨立伺服器](#shared-feature)。

+ 請勿安裝容錯移轉叢集上。 用來隔離 R 和 Python 處理程序的安全性機制與不相容的 Windows Server 容錯移轉叢集環境。

+ 請勿在網域控制站上安裝。 Machine Learning 服務的部分安裝程式將會失敗。

+ 避免在相同電腦上安裝獨立式和資料庫執行個體。 在獨立伺服器將會競爭相同的資源，進而破壞的兩個安裝效能。


## <a name="command-line-arguments"></a>命令列引數

必要的因為會授權詞彙合約功能引數。 

透過命令提示字元安裝時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援使用 /Q 參數的完整無訊息模式或使用 /QS 參數的簡單無訊息模式。 /QS 參數只會顯示進度、不接受任何輸入，而且不會顯示任何遇到的錯誤訊息。 只有當您指定 /Action=install 時，才支援 /QS 參數。

| 引數 | 描述 |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 會安裝在資料庫版本：SQL Server 2017 Machine Learning 服務 （資料庫） 或 SQL Server 2016 R Services （資料庫）。  |
| /FEATURES = SQL_INST_MR | 適用於僅 SQL Server 2017。 將它搭配 AdvancedAnalytics。 會安裝 （資料庫內） R 功能，包括 Microsoft R Open 和專屬的 R 套件。 SQL Server 2016 R Services 功能是 R 專用，因此沒有任何參數，該版本。|
| /FEATURES = SQL_INST_MPY | 適用於僅 SQL Server 2017。 將它搭配 AdvancedAnalytics。 會安裝 Python （資料庫） 的功能，包括 Anaconda 和專屬的 Python 套件。 |
| /FEATURES = SQL_SHARED_MR | 會安裝獨立版本的 R 功能：SQL Server 2017 Machine Learning 伺服器 （獨立式） 或 SQL Server 2016 R Server （獨立式）。 未繫結至資料庫引擎執行個體的 「 共用的功能 」 的獨立伺服器。|
| /FEATURES = SQL_SHARED_MPY | 適用於僅 SQL Server 2017。 會安裝獨立版本的 Python 功能：SQL Server 2017 Machine Learning 伺服器 （獨立式）。 未繫結至資料庫引擎執行個體的 「 共用的功能 」 的獨立伺服器。|
| /IACCEPTROPENLICENSETERMS  | 表示您接受授權條款，以使用開放原始碼 R 元件。 |
| /IACCEPTPYTHONLICENSETERMS | 表示您接受授權條款，以使用 Python 元件。 |
| /IACCEPTSQLSERVERLICENSETERMS | 表示您接受授權合約，以使用 SQL Server。|
| /MRCACHEDIRECTORY | 離線安裝程式，設定包含 R 元件 CAB 檔案的資料夾。 |
| / MPYCACHEDIRECTORY | 保留供日後使用。 使用 %TEMP%來儲存 Python 元件 CAB 檔案安裝在沒有網際網路連線的電腦上。 |


## <a name="indb"></a> 在資料庫執行個體安裝

在資料庫內分析可供 database engine 執行個體，加入所需**AdvancedAnalytics**功能到您的安裝。 您可以使用進階分析，來安裝資料庫引擎執行個體或[將它新增至現有的執行個體](#add-existing)。 

若要檢視進度資訊，而不需要互動式螢幕上的提示，請使用 /qs 引數。

> [!IMPORTANT]
> 安裝完成後，維持兩個額外的設定步驟。 整合不完整，直到這些工作會執行。 請參閱[後續安裝工作](#post-install)如需相關指示。

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017： 資料庫引擎，使用 Python 和 R 進行進階分析

對於資料庫引擎執行個體並行安裝，提供執行個體名稱和系統管理員 (Windows) 登入。 包含安裝核心和語言元件，以及所有的授權條款的接受度的功能。

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

這個相同的命令，但使用 SQL Server 上的登入資料庫引擎，使用混合驗證。

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

這個範例是 Python，顯示您可以藉由略過功能加入一種語言。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016： 資料庫引擎和使用 R 的進階的分析

此命令是相同的 SQL Server 2017 中，但是不會的 Python 項目，並不是 SQL Server 2016 安裝程式。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> 後續安裝組態 （必要）

適用於資料庫只能安裝。

安裝程式完成時，您會有使用 R 和 Python，Microsoft R 和 Python 套件、 Microsoft R Open，Anaconda、 工具、 範例和指令碼屬於散發資料庫引擎執行個體。 

兩個的更多工作才能完成安裝程序：

1. 重新啟動 database engine 服務。

1. 您可以使用此功能之前，請啟用外部指令碼。 請依照下列中的指示[安裝 SQL Server 2017 Machine Learning 服務 （資料庫）](sql-machine-learning-services-windows-install.md)在下一個步驟。 

適用於 SQL Server 2016，請改用這篇文章[安裝 SQL Server 2016 R Services （資料庫）](sql-r-services-windows-install.md)。

## <a name="add-existing"></a> 加入現有的資料庫引擎執行個體中的進階的分析

當資料庫內進階的分析加入現有的資料庫引擎執行個體，提供執行個體名稱。 比方說，如果您先前安裝的 SQL Server 2017 資料庫引擎和 Python，您可以使用此命令以新增。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> 無訊息安裝

無訊息安裝會抑制.cab 檔案位置的檢查。 基於這個理由，您必須指定.cab 檔來解除封裝的位置。 對於 Python，封包檔必須位於 %temp *。 針對 R，您可以設定資料夾使用您的路徑可以為此的暫存目錄。
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a> 獨立伺服器安裝

未繫結至資料庫引擎執行個體的 「 共用的功能 」 的獨立伺服器。 下列範例示範這兩個版本的有效語法。

SQL Server 2017 支援 Python 和 R，在獨立伺服器上：

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 是僅限 R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

安裝程式完成時，您會有伺服器、 Microsoft 套件、 開放原始碼散發套件的 R 和 Python，工具、 範例和屬於散發的指令碼。 

若要開啟 R 主控台視窗中，移至 \Program files\Microsoft SQL Server\140 （或 130） \R_SERVER\bin\x64，然後按兩下**RGui.exe**。 不熟悉 R 嗎？ 請嘗試本教學課程：[R 的基本命令和 RevoScaleR 函式：25 的常見範例](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)。

若要開啟 Python 命令，請移至 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\bin\x64，然後按兩下**python.exe**。

## <a name="get-help"></a>取得說明

需要安裝或升級的說明嗎？ 如需常見問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查的執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續步驟

R 開發人員可以開始使用一些簡單的範例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以了解如何使用 SQL Server 中的 Python，遵循這些教學課程：

+ [教學課程：在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視機器學習服務依據真實世界案例的範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。