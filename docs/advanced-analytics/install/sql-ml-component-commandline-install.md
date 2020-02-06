---
title: 從命令提示字元安裝
description: 執行 SQL Server 命令列安裝程式，以將 R 語言和 Python 整合新增至 SQL Server 的資料庫引擎執行個體。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2bc231a064862c5e2a16f60d85a5166fd4765566
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727586"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>從命令列安裝 SQL Server 機器學習 R 和 Python 元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供從命令列安裝 SQL Server 機器學習服務元件的指示：

+ [新的資料庫內執行個體](#indb)
+ [新增至現有的資料庫引擎執行個體](#add-existing)
+ [無訊息安裝](#silent)
+ [新獨立伺服器](#shared-feature)

您可以指定與安裝程式使用者介面的無訊息、基本或完整互動。 本文補充[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，涵蓋 R 和 Python 機器學習元件唯一的參數。

## <a name="pre-install-checklist"></a>預先安裝檢查清單

+ 然後透過具有更高權限的命令提示字元來執行命令。 

+ 資料庫引擎執行個體是資料庫內安裝的必要項目。 您無法只安裝 R 或 Python 功能，雖然您可以[藉由累加方式將其新增至現有的執行個體](#add-existing)。 如果您只想要不含資料庫引擎的 R 和 Python，請安裝[獨立伺服器](#shared-feature)。

+ 請勿在容錯移轉叢集上安裝。 用來隔離 R 和 Python 程序的安全性機制不相容於 Windows Server 容錯移轉叢集環境。

+ 請勿在網域控制站上安裝。 安裝程式的機器學習服務部分將會失敗。

+ 請避免在同一部電腦上安裝獨立和資料庫內執行個體。 獨立伺服器會爭用相同資源，而損害這兩個安裝的效能。


## <a name="command-line-arguments"></a>命令列引數

FEATURES 引數是必要的，如同授權條款合約。 

透過命令提示字元安裝時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援使用 /Q 參數的完整無訊息模式或使用 /QS 參數的簡單無訊息模式。 /QS 參數只會顯示進度、不接受任何輸入，而且不會顯示任何遇到的錯誤訊息。 只有當您指定 /Action=install 時，才支援 /QS 參數。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
| 引數 | 描述 |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 安裝資料庫內版本：SQL Server R Services (資料庫內)。  |
| /FEATURES = SQL_SHARED_MR | 安裝獨立版本的 R 功能：Microsoft R Server (獨立式)。 獨立伺服器是指未繫結至資料庫引擎執行個體的「共用功能」。|
| /IACCEPTROPENLICENSETERMS  | 表示您已接受授權合約以使用開放原始碼 R 元件。 |
| /IACCEPTPYTHONLICENSETERMS | 表示您已接受授權合約以使用 Python 元件。 |
| /IACCEPTSQLSERVERLICENSETERMS | 表示您已接受使用 SQL Server 的授權條款。|
| /MRCACHEDIRECTORY | 針對離線安裝，會設定包含 R 元件 CAB 檔案的資料夾。 |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
| 引數 | 描述 |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 安裝資料庫內版本：SQL Server 機器學習服務 (資料庫內)。  |
| /FEATURES = SQL_INST_MR | 將此與 AdvancedAnalytics 配對。 安裝 (資料庫內) R 功能，包括 Microsoft R Open 和專屬的 R 套件。 |
| /FEATURES = SQL_INST_MPY | 將此與 AdvancedAnalytics 配對。 安裝 (資料庫內) Python 功能，包括 Anaconda 和專屬 Python 套件。 |
| /FEATURES = SQL_SHARED_MR | 安裝獨立版本的 R 功能：SQL Server Machine Learning Server (獨立式)。 獨立伺服器是指未繫結至資料庫引擎執行個體的「共用功能」。|
| /FEATURES = SQL_SHARED_MPY | 安裝獨立版本的 Python 功能：SQL Server Machine Learning Server (獨立式)。 獨立伺服器是指未繫結至資料庫引擎執行個體的「共用功能」。|
| /IACCEPTROPENLICENSETERMS  | 表示您已接受授權合約以使用開放原始碼 R 元件。 |
| /IACCEPTPYTHONLICENSETERMS | 表示您已接受授權合約以使用 Python 元件。 |
| /IACCEPTSQLSERVERLICENSETERMS | 表示您已接受使用 SQL Server 的授權條款。|
| /MRCACHEDIRECTORY | 針對離線安裝，會設定包含 R 元件 CAB 檔案的資料夾。 |
| /MPYCACHEDIRECTORY | 保留供未來使用。 請使用 %TEMP% 來儲存 Python 元件 CAB 檔案，以在沒有網際網路連線的電腦上進行安裝。 |
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
| 引數 | 描述 |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 安裝資料庫內版本：SQL Server 機器學習服務 (資料庫內)。  |
| /FEATURES = SQL_INST_MR | 將此與 AdvancedAnalytics 配對。 安裝 (資料庫內) R 功能，包括 Microsoft R Open 和專屬的 R 套件。 |
| /FEATURES = SQL_INST_MPY | 將此與 AdvancedAnalytics 配對。 安裝 (資料庫內) Python 功能，包括 Anaconda 和專屬 Python 套件。 |
| /FEATURES = SQL_INST_MJAVA | 將此與 AdvancedAnalytics 配對。 安裝 (資料庫內) JAVA 功能，包括 Open JRE。 |
| /FEATURES = SQL_SHARED_MR | 安裝獨立版本的 R 功能：SQL Server Machine Learning Server (獨立式)。 獨立伺服器是指未繫結至資料庫引擎執行個體的「共用功能」。|
| /FEATURES = SQL_SHARED_MPY | 安裝獨立版本的 Python 功能：SQL Server Machine Learning Server (獨立式)。 獨立伺服器是指未繫結至資料庫引擎執行個體的「共用功能」。|
| /IACCEPTROPENLICENSETERMS  | 表示您已接受授權合約以使用開放原始碼 R 元件。 |
| /IACCEPTPYTHONLICENSETERMS | 表示您已接受授權合約以使用 Python 元件。 |
| /IACCEPTSQLSERVERLICENSETERMS | 表示您已接受使用 SQL Server 的授權條款。|
| /MRCACHEDIRECTORY | 針對離線安裝，會設定包含 R 元件 CAB 檔案的資料夾。 |
| /MPYCACHEDIRECTORY | 保留供未來使用。 請使用 %TEMP% 來儲存 Python 元件 CAB 檔案，以在沒有網際網路連線的電腦上進行安裝。 |
::: moniker-end

## <a name="indb"></a> 資料庫內執行個體安裝

資料庫內分析適用於資料庫引擎執行個體，這是將 **AdvancedAnalytics** 功能新增至安裝時的必要項目。 您可以使用進階分析安裝資料庫引擎執行個體，或[將其新增至現有執行個體](#add-existing)。 

若要在沒有互動式工具提示的情況下檢視進度資訊，請使用 /qs 引數。

> [!IMPORTANT]
> 安裝之後，還有兩個額外的設定步驟。 在執行這些工作後，整合才會完成。 如需指示，請參閱[安裝後工作](#post-install)。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
### <a name="sql-server-machine-learning-services-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server Machine Learning 服務：資料庫引擎、使用 Python 和 R 的進階分析

針對資料庫引擎執行個體的並行安裝，請提供執行個體名稱和系統管理員 (Windows) 登入。 包含安裝核心和語言元件的功能，並接受所有授權條款。

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

這是相同的命令，但在使用混合式驗證的資料庫引擎上具有 SQL Server 登入。

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

此範例僅適用於 Python，顯示您可以藉由省略功能來新增一種語言。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
### <a name="sql-server-r-services-database-engine-and-advanced-analytics-with-r"></a>SQL Server R Services：使用 R 的資料庫引擎和進階分析

針對資料庫引擎執行個體的並行安裝，請提供執行個體名稱和系統管理員 (Windows) 登入。 包含安裝核心和語言元件的功能，並接受所有授權條款。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```
::: moniker-end

## <a name="post-install"></a> 安裝後設定 (必要)

僅適用於資料庫內安裝。

當安裝程式完成時，您會有一個具有 R 和 Python 的資料庫引擎執行個體、Microsoft R 和 Python 套件、Microsoft R Open、Anaconda、工具、範例，以及屬於散發套件一部分的指令碼。 

還需要執行兩個步驟才能完成安裝：


::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. 重新啟動資料庫引擎服務。

1. SQL Server Machine Learning 服務：您必須先啟用外部指令碼，才能使用此功能。 遵循[安裝 SQL Server Machine Learning 服務 (資料庫內)](sql-machine-learning-services-windows-install.md) 中的指示作為下一個步驟。 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. 重新啟動資料庫引擎服務。

1. SQL Server R 服務：您必須先啟用外部指令碼，才能使用此功能。 遵循[安裝 SQL Server R Services (資料庫內)](sql-r-services-windows-install.md) 中的指示作為下一個步驟。 
::: moniker-end

## <a name="add-existing"></a> 將進階分析新增至現有的資料庫引擎執行個體

將資料庫內的進階分析新增至現有資料庫引擎執行個體時，請提供執行個體名稱。 例如，如果您先前安裝了 SQL Server 2017 或更新版本的資料庫引擎和 Python，則可以使用此命令來新增 R。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```

## <a name="silent"></a> 無訊息安裝

無訊息安裝會隱藏 .cab 檔案位置的檢查。 基於此原因，您必須指定要解壓縮 .cab 檔案的位置。 針對 Python，CAB 檔案必須位於 %TEMP*。 針對 R，您可以使用此項目的暫存目錄來設定資料夾路徑。
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a> 獨立伺服器安裝

獨立伺服器是指未繫結至資料庫引擎執行個體的「共用功能」。 下列範例顯示獨立伺服器安裝的有效語法。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Server 支援獨立伺服器上的 Python 和 R：

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R 伺服器僅適用於 R：

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end

安裝程式完成時，您會有一部伺服器、Microsoft 套件、R 和 Python 的開放原始碼發佈、工具、範例，以及屬於散發套件一部分的指令碼。 

若要開啟 R 主控台視窗，請前往 `\Program files\Microsoft SQL Server\150 (or 140/130)\R_SERVER\bin\x64`，然後按兩下 [RGui.exe]  。 不熟悉 R 嗎？ 嘗試此教學課程：[基本 R 命令和 RevoScaleR 函式：25 個常見範例](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)。

若要開啟 Python 命令，請前往 `\Program files\Microsoft SQL Server\150 (or 140)\PYTHON_SERVER\bin\x64`，然後按兩下 [python.exe]  。

## <a name="get-help"></a>取得說明

需要安裝或升級的協助嗎？ 如需常見問題和已知問題的解答，請參閱下文：

* [升級和安裝常見問題集 - Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>後續步驟

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../tutorials/quickstart-r-create-script.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [教學課程：在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視以真實世界案例為基礎的機器學習範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。