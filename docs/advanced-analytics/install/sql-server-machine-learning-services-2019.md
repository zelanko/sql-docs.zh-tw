---
title: SQL Server 2019 中的差異
description: 在 SQL Server 2019 preview 版本中, 瞭解 R 和 Python 的新功能 SQL Server 機器學習服務延伸模組。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 218ae9bd0685370f38942592fd32da75272fbcac
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470302"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>SQL Server 2019 中 SQL Server Machine Learning 服務安裝的差異  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在 Windows 上, SQL Server 2019 安裝程式會變更外部進程的隔離機制。 這項變更會以[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)取代本機背景工作帳戶, 這是在 Windows 上執行的用戶端應用程式的隔離技術。 

系統管理員沒有任何特定的動作專案, 因此無法進行修改。 在新的或升級的伺服器上, 從[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)執行的所有外部腳本和程式碼都會自動遵循新的隔離模式。 

總結而言, 此版本的主要差異如下:

+ **SQL 受限使用者群組 (SQLRUserGroup)** 下的本機使用者帳戶不再建立或用來執行外部進程。 AppContainers 取代它們。
+ **SQLRUserGroup**成員資格已變更。 成員資格只包含 SQL Server Launchpad 服務帳戶, 而不是多個本機使用者帳戶。 R 和 Python 進程現在會在啟動列服務身分識別下執行, 並透過 AppContainers 隔離。

雖然隔離模式已變更, 但安裝精靈和命令列參數在 SQL Server 2019 中保持不變。 如需安裝的說明, 請參閱[安裝 SQL Server Machine Learning 服務](sql-machine-learning-services-windows-install.md)。

## <a name="about-appcontainer-isolation"></a>關於 AppContainer 隔離

在舊版中, **SQLRUserGroup**包含了用來隔離和執行外部進程的本機 Windows 使用者帳戶 (MSSQLSERVER00-MSSQLSERVER20) 集區。 當需要外部進程時, SQL Server Launchpad 服務會取得可用的帳戶, 並使用它來執行處理常式。 

在 SQL Server 2019 中, 安裝程式不會再建立本機背景工作帳戶。 相反地, 隔離是透過[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)來達成。 在執行時間, 在預存程式或查詢中偵測到內嵌腳本或程式碼時, SQL Server 會使用延伸模組特定啟動器的要求來呼叫啟動控制板。 啟動列會在其身分識別的進程中叫用適當的執行時間環境, 並具現化 AppContainer 以包含它。 這種變更很有用, 因為已不再需要本機帳戶和密碼管理。 此外, 在禁止本機使用者帳戶的安裝上, 刪除本機使用者帳戶相依性表示您現在可以使用這項功能。

AppContainers 由 SQL Server 實作為內部機制。 雖然您不會在進程監視器中看到 AppContainers 的實體辨識項, 但是您可以在安裝程式所建立的輸出防火牆規則中找到它們, 以避免進程進行網路呼叫。

## <a name="firewall-rules-created-by-setup"></a>安裝程式所建立的防火牆規則

根據預設, SQL Server 會藉由建立防火牆規則來停用輸出連線。 在過去, 這些規則是以本機使用者帳戶為基礎, 其中安裝程式為**SQLRUserGroup**拒絕對其成員進行網路存取的一個輸出規則 (每個背景工作帳戶都列為 rule_ 的本機原則。 

在移至 AppContainers 的過程中, 有一個以 AppContainer Sid 為基礎的新防火牆規則: 一個是針對 SQL Server 安裝程式所建立的20個 AppContainers 中的每一個。 防火牆規則名稱的命名慣例是**SQL Server 實例 MSSQLSERVER 中的 appcontainer-00 封鎖網路存取**, 其中00是 appcontainer 的數目 (預設為 00-20), 而 MSSQLSERVER 是 SQL Server 實例的名稱。 

> [!Note]
> 如果需要網路呼叫, 您可以停用 Windows 防火牆中的輸出規則。

## <a name="program-file-permissions"></a>程式檔案許可權

如同先前的版本, **SQLRUserGroup**會繼續提供 SQL Server **Binn**、 **R_SERVICES**和**PYTHON_SERVICES**目錄中可執行檔的讀取和執行許可權。 在此版本中, **SQLRUserGroup**的唯一成員是 SQL Server Launchpad 服務帳戶。  當啟動列服務啟動 R 或 Python 執行環境時, 進程會以啟動控制服務的方式執行。

## <a name="implied-authentication"></a>隱含驗證

如先前所述, 當腳本或程式碼 SQL Server 必須使用受信任的驗證來抓取資料或資源時,*隱含驗證*仍然需要進行其他設定, 才能進行其他設定。 額外的設定牽涉到建立**SQLRUserGroup**的資料庫登入, 其唯一成員現在是單一 SQL Server Launchpad 服務帳戶, 而不是多個背景工作帳戶。 如需這項工作的詳細資訊, 請參閱[將 SQLRUserGroup 新增為資料庫使用者](../security/create-a-login-for-sqlrusergroup.md)。


## <a name="symbolic-link-created-by-setup"></a>安裝程式所建立的符號連結

在 SQL Server 安裝程式中, 會建立與目前預設**R_SERVICES**和**PYTHON_SERVICES**的符號連結。 如果您不想要建立此連結, 替代方法是將「所有應用程式套件」讀取權限授與給資料夾的階層。


## <a name="see-also"></a>另請參閱

+ [在 Windows 上安裝 SQL Server Machine Learning 服務](sql-machine-learning-services-windows-install.md)

+ [在 Linux 上安裝 SQL Server 2019 Machine Learning 服務](../../linux/sql-server-linux-setup-machine-learning.md)
