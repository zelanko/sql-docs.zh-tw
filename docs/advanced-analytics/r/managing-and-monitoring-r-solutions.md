---
title: 管理和整合機器學習服務工作負載
description: 身為 SQL Server DBA, 請參閱在資料庫引擎實例上部署機器學習 R 和 Python 子系統的系統管理工作。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: fab91e142fad3bcb1ce23816d6705f7a7d208851
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345315"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>在 SQL Server 上管理和整合機器學習服務工作負載
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文適用于負責在支援多個工作負載的伺服器資產上部署有效率的資料科學基礎結構的 SQL Server 資料庫管理員。 它會在 SQL Server 上, 將 R 和 Python 程式碼執行管理的相關管理問題空間框架在一起。 

## <a name="what-is-feature-integration"></a>什麼是功能整合

R 和 Python 機器學習是由[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)提供, 做為資料庫引擎實例的延伸模組。 整合主要是透過安全性層級和資料定義語言, 如下所示:

+ 預存程式具備接受 R 和 Python 程式碼做為輸入參數的能力。 開發人員和資料科學家可以使用[系統預存](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017)程式, 或建立包裝其程式碼的自訂程式。
+ 可以取用先前定型之資料模型的 t-sql 函數 (亦即[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql))。 這項功能可透過 T-sql 取得。 因此, 它可以在未安裝機器學習擴充功能的系統上呼叫。
+ 現有的資料庫登入和以角色為基礎的許可權涵蓋使用相同資料的使用者叫用腳本。 一般的規則是, 如果使用者無法透過查詢存取資料, 他們就無法透過腳本存取它。

## <a name="feature-availability"></a>功能可用性

R 和 Python 整合會透過連續的步驟提供使用。 當您將[ **Machine Learning Services**功能包含或加入](../install/sql-machine-learning-services-windows-install.md)至 database engine 實例時, 第一個就是設定。 在後續步驟中, 您必須在 database engine 實例上啟用外部腳本 (預設為關閉)。

此時, 只有資料庫管理員具有建立和執行外部腳本、加入或刪除封裝, 以及建立預存程式和其他物件的完整許可權。

所有其他使用者都必須被授與 [執行任何外部腳本] 許可權。 其他[標準資料庫許可權](../security/user-permission.md)會決定使用者是否可以建立物件、執行腳本、取用序列化和定型的模型等等。 

## <a name="resource-allocation"></a>資源配置

叫用外部處理的預存程式和 T-SQL 查詢會使用預設資源集區可用的資源。 做為預設設定的一部分, 系統會允許外部進程 (例如 R 和 Python 會話) 在主機系統上最多 20% 的總記憶體。 

如果您想要重新調整資源, 您可以修改預設集區, 並對在該系統上執行的機器學習服務工作負載進行相對應的影響。

另一個選項是建立自訂外部資源集區, 以捕獲源自特定時間間隔內特定程式、主機或活動的會話。 如需詳細資訊, 請參閱[資源管理以修改 R 和 Python 執行的資源層級](../administration/resource-governance.md)和[如何建立資源集](../administration/how-to-create-a-resource-pool.md)區, 以取得逐步指示。

## <a name="isolation-and-containment"></a>隔離和內含專案

處理架構的設計是為了隔離外部腳本與核心引擎處理。 R 和 Python 腳本會在 [本機背景工作帳戶] 下以個別進程的形式執行。 在 [工作管理員] 中, 您可以監視 R 和 Python 進程, 在低許可權的本機使用者帳戶下執行, 與 SQL Server 服務帳戶不同。 

在個別的低許可權帳戶中執行 R 和 Python 進程具有下列優點:

+ 隔離 R 和 Python 會話的核心引擎程式您可以終止 R 或 Python 進程, 而不會影響核心資料庫作業。 

+ 減少主機電腦上外部腳本執行時間處理常式的許可權。

系統會在安裝期間建立最低許可權帳戶, 並將其放在名為**SQLRUserGroup**的 Windows*使用者帳戶集*區中。 根據預設, 此群組具有在 SQL Server 的 R 和 Python 的 program 資料夾中使用可執行檔、程式庫和內建資料集的許可權。 

身為 DBA, 您可以使用 SQL Server 資料安全性來指定有權執行腳本的人員, 而作業中所使用的資料則是以控制透過 T-SQL 查詢存取的相同安全性角色來管理。 身為系統管理員, 您可以藉由建立 Acl, 明確拒絕對本機伺服器上的機密資料進行**SQLRUserGroup**存取。

>[!NOTE]
> 根據預設, **SQLRUserGroup**沒有 SQL Server 本身的登入或許可權。 如果背景工作帳戶需要登入來進行資料存取, 您就必須自行建立。 特別呼叫建立登入的案例, 是為了支援來自執行中腳本的要求、資料庫引擎實例上的資料或作業 (當使用者身分識別為 Windows 使用者, 且連接字串指定信任的使用者) 時。 如需詳細資訊, 請參閱[將 SQLRUserGroup 新增為資料庫使用者](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

## <a name="disable-script-execution"></a>停用腳本執行

在腳本失控的情況下, 您可以停用所有腳本執行, 並反轉先前執行的步驟, 以在一開始就啟用外部腳本。

1. 在 SQL Server Management Studio 或其他查詢工具中, 執行此命令以`external scripts enabled`將設定為0或 FALSE。

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. 重新開機資料庫引擎服務。

解決問題之後, 如果您想要在資料庫引擎實例上繼續 R 和 Python 腳本支援, 請記得在實例上重新啟用腳本執行。 如需詳細資訊, 請參閱[啟用腳本執行](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>擴充功能

資料科學通常會引進封裝部署和管理的新需求。 對於資料科學家而言, 在自訂解決方案中利用開放原始碼和協力廠商套件是常見的作法。 其中有些封裝會相依于其他套件, 在此情況下, 您可能需要評估並安裝多個套件, 以達到您的目標。

身為負責伺服器資產的 DBA, 將任意的 R 和 Python 套件部署到實際執行的伺服器上, 代表不熟悉的挑戰。 在新增封裝之前, 您應該先評估外部套件所提供的功能是否真的需要, 而在 SQL Server 安裝程式所安裝的內建[R 語言](r-libraries-and-data-types.md)和[Python 程式庫](../python/python-libraries-and-data-types.md)中, 沒有對等的。 

做為伺服器套件安裝的替代方案, 資料科學家可能可以[在外部工作站上建立及執行解決方案](../r/set-up-a-data-science-client.md)、從 SQL Server 抓取資料, 但在工作站上本機執行所有分析, 而不是在伺服器上執行直接. 

如果您接著判斷需要外部程式庫函式, 而且不會對伺服器作業或資料整體造成風險, 您可以選擇多個方法來新增封裝。 在大部分情況下, 需要有系統管理員許可權, 才能將封裝新增至 SQL Server。 若要深入瞭解, 請參閱[在 SQL Server 中安裝 Python 套件](../python/install-additional-python-packages-on-sql-server.md)和[在 SQL Server 中安裝 R 套件](install-additional-r-packages-on-sql-server.md)。

> [!NOTE]
> 針對 R 封裝, 如果您使用替代方法, 則不需要伺服器管理員許可權就能安裝套件。 如需詳細資訊, 請參閱[在 SQL Server 中安裝 R 套件](install-additional-r-packages-on-sql-server.md)。

## <a name="monitoring-script-execution"></a>監視腳本執行

在中[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行的 R 和 Python 腳本會[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]由介面啟動。 不過, 啟動列不會個別進行資源管理或監視, 因為它是由 Microsoft 提供的安全服務, 會適當地管理資源。

在啟動列服務下執行的外部腳本會使用[Windows 工作物件](/windows/desktop/ProcThread/job-objects)進行管理。 作業物件可讓您將處理序群組當作一個單位來管理。 每個作業物件都是階層式物件，並控制與其關聯之所有處理序的屬性。 在作業物件上執行的作業會影響與該作業物件關聯的所有處理序。

因此，如果您需要終止一個與某個物件關聯的作業，請注意，所有相關的處理序也將一併終止。 如果您正在執行指派給 Windows 作業物件的 R 指令碼，而該指令碼執行必須終止的相關 ODBC 作業，則父系 R 指令碼處理序也將一併終止。

如果您啟動使用平行處理的外部腳本, 則單一 Windows 工作物件會管理所有平行子進程。

若要判斷處理序是否是在作業中執行，請使用 `IsProcessInJob` 函數。

## <a name="next-steps"></a>後續步驟

+ 回顧擴充性[架構](../concepts/extensibility-framework.md)的概念和元件, 以及更多背景的[安全性](../concepts/security.md)。

+ 在安裝功能的過程中, 您可能已經熟悉使用者資料存取控制, 但如果沒有, 請參閱授與[使用者權限以 SQL Server 機器學習](../security/user-permission.md)服務, 以取得詳細資訊。 

+ 瞭解如何調整計算密集型機器學習服務工作負載的系統資源。 如需詳細資訊, 請參閱[如何建立資源集](../administration/how-to-create-a-resource-pool.md)區。
