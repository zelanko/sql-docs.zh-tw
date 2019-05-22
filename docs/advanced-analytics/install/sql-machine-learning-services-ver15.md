---
title: SQL Server 2019-SQL Server Machine Learning 服務中的差異
description: 了解 R 和 Python 的 SQL Server 機器學習服務擴充功能在 SQL Server 2019 的預覽版本的最新消息。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3d549bdc96e09ed0b9b0235ada51274201f1b91a
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994228"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>在 SQL Server Machine Learning 服務安裝在 SQL Server 2019 的差異  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 Windows、 SQL Server 2019 安裝程式會變更外部處理序隔離機制。 這項變更會取代本機的背景工作帳戶[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)，隔離技術，在 Windows 上執行的用戶端應用程式。 

沒有特定的動作項目，因為修改系統管理員。 在新的或已升級伺服器，所有外部指令碼和程式碼從執行[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)自動遵循新的隔離模型。 

摘要說明，在此版本中的主要差異如下：

+ 本機使用者帳戶之下**SQL 限制使用者群組 (SQLRUserGroup)** 不會再建立或用來執行外部處理序。 AppContainers 取代它們。
+ **SQLRUserGroup**成員資格有所變更。 而不是多個本機使用者帳戶，成員資格包含只是 SQL Server Launchpad 服務帳戶。 R 和 Python 處理程序現在在 Launchpad 服務身分識別，透過 AppContainers 隔離下執行。

雖然隔離模型已變更時，安裝精靈和命令列參數會保持相同的 SQL Server 2019。 如需安裝的說明，請參閱[安裝 SQL Server Machine Learning 服務](sql-machine-learning-services-windows-install.md)。

## <a name="about-appcontainer-isolation"></a>關於 AppContainer 隔離

在舊版中， **SQLRUserGroup**所包含的本機 Windows 使用者帳戶 (MSSQLSERVER00 MSSQLSERVER20) 可用來隔離及執行外部處理序集區。 當外部處理序已有需要時 SQL Server Launchpad 服務會使用可用的帳戶，並且使用它來執行處理程序。 

在 SQL Server 2019，安裝程式不會再建立本機的背景工作帳戶。 相反地，透過來達成隔離[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)。 在執行階段，當內嵌指令碼或程式碼中偵測到預存程序或查詢，在 SQL Server 會呼叫啟動控制板，並要求延伸模組特定程式啟動器。 啟動控制板叫用其身分的處理序中的適當的執行階段環境，並包含該 AppContainer 具現化。 這項變更是有幫助，因為不再需要本機帳戶和密碼管理。 此外，其中禁止使用本機使用者帳戶的安裝，刪除本機使用者帳戶相依性表示您現在可以使用這項功能。

實作 SQL server 時，AppContainers 會是內部的機制。 雖然您不會看到 AppContainers Process Monitor 中的實體的辨識項，您可以找到它們，以防止處理程序進行網路呼叫的安裝程式所建立的輸出防火牆規則中。

## <a name="firewall-rules-created-by-setup"></a>安裝程式所建立的防火牆規則

根據預設，SQL Server 會停用輸出連線，藉由建立防火牆規則。 在過去，這些規則以本機使用者帳戶，安裝程式建立的一項輸出規則的所在**SQLRUserGroup** ，拒絕網路存取其成員 （每個背景工作帳戶已列為 rule_ 受到本機原則。 

移至 AppContainers 的一部分，有新 AppContainer Sid 為基礎的防火牆規則： 一個用於每個 20 AppContainers 建立 SQL Server 安裝程式。 防火牆規則名稱的命名慣例**AppContainer 00 封鎖網路存取 SQL Server 執行個體 MSSQLSERVER 中**其中 00 AppContainer (00-20 預設)，數目，是 MSSQLSERVER 是 SQL 的名稱伺服器執行個體。 

> [!Note]
> 如果需要網路呼叫，您可以停用 Windows 防火牆中的輸出規則。

## <a name="program-file-permissions"></a>程式檔案的權限

如同舊版本中， **SQLRUserGroup**會繼續提供讀取和執行 SQL Server 中的可執行檔的權限**Binn**， **R_SERVICES**，和**PYTHON_SERVICES**目錄。 在這一版的唯一成員**SQLRUserGroup**是 SQL Server Launchpad 服務帳戶。  Launchpad 服務啟動時 R 或 Python 執行環境，LaunchPad 服務會執行此程序。

## <a name="implied-authentication"></a>隱含驗證

因為之前，其他設定仍然需要*隱含的驗證*的指令碼或程式碼有具有連回 SQL Server 擷取資料或資源使用受信任的驗證。 額外的設定牽涉到建立的資料庫登入**SQLRUserGroup**，其唯一的成員現在是單一的 SQL Server Launchpad 服務帳戶，而不是多個背景工作帳戶。 如需有關這項工作的詳細資訊，請參閱 <<c0> [ 為資料庫使用者的新增 SQLRUserGroup](../security/add-sqlrusergroup-to-database.md)。


## <a name="symbolic-link-created-by-setup"></a>安裝程式所建立的符號連結

為目前的預設值建立符號連結**R_SERVICES**並**PYTHON_SERVICES**做為 SQL Server 安裝程式的一部分。 如果您不想要建立此連結，或者是 'all application packages' 的讀取權限授與至資料夾階層。


## <a name="see-also"></a>另請參閱

+ [安裝 SQL Server Machine Learning 在 Windows 上的服務](sql-machine-learning-services-windows-install.md)

+ [在 Linux 上安裝 SQL Server 2019 Machine Learning 服務](../../linux/sql-server-linux-setup-machine-learning.md)
