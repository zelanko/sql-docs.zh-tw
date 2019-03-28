---
title: 管理並整合 SQL Server 機器學習服務-機器學習工作負載
description: SQL Server DBA，檢閱部署機器學習服務 R 和 Python 的子系統，database engine 執行個體上的系統管理工作。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c9b1b4eca18a9d4d8d1819eee399676046cc9d78
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510065"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>管理並整合 SQL Server 上的機器學習工作負載
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是適用於 SQL Server 資料庫管理員負責部署有效率的資料科學基礎結構上支援多個工作負載的伺服器資產。 框架的系統管理的問題空間相關的管理 R 和 Python 程式碼在 SQL Server 上的執行。 

## <a name="what-is-feature-integration"></a>功能整合是什麼

R 和 Python 機器學習服務由提供[SQL Server 機器學習服務](../what-is-sql-server-machine-learning.md)做為資料庫引擎執行個體的延伸。 整合是主要是透過安全性層級和資料定義語言中，彙總，如下所示：

+ 預存程序便有能力能夠接受 R 和 Python 程式碼作為輸入的參數。 開發人員和資料科學家可以使用[系統預存程序](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017)或建立包裝其程式碼的自訂程序。
+ T-SQL 函式 (亦即[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql))，可以使用之前已培訓的資料模型。 這項功能可透過 T-SQL。 因此，特別是沒有的機器學習服務延伸模組安裝在系統上可以呼叫它。
+ 現有的資料庫登入和以角色為基礎的權限涵蓋使用者叫用指令碼使用相同的資料。 一般而言，如果使用者無法存取資料，透過查詢時，就無法存取它透過指令碼是。

## <a name="feature-availability"></a>功能可用性

R 和 Python 整合會變成可透過一連串的步驟。 第一個是安裝程式，當您[包含或加入**Machine Learning 服務**](../install/sql-machine-learning-services-windows-install.md)資料庫引擎執行個體的功能。 後續步驟中，您必須啟用外部指令碼 （它預設為關閉） 資料庫引擎執行個體上。

到目前為止，只有資料庫管理員擁有完整權限建立和執行外部指令碼、 加入或刪除封裝，並建立預存程序及其他物件。

所有其他使用者必須具有 EXECUTE ANY EXTERNAL SCRIPT 權限。 額外[標準的資料庫權限](../security/user-permission.md)判斷使用者是否可以建立物件、 執行指令碼、 使用序列化和定型模型，以及等。 

## <a name="resource-allocation"></a>資源配置

預存程序和叫用外部處理的 T-SQL 查詢使用預設資源集區可用的資源。 預設組態的一部分，例如 R 和 Python 的工作階段的外部處理序允許最多 20%的總記憶體主機系統上。 

如果您想要重新調整資源，您可以修改預設集區，與該系統上執行的機器學習工作負載中對應的效果。

另一個選項是建立自訂的外部資源集區，來擷取源自於特定的程式、 主機或特定時間間隔期間所發生的活動的工作階段。 如需詳細資訊，請參閱 <<c0> [ 若要修改 R 和 Python 執行資源層級的資源控管](../administration/resource-governance.md)並[如何建立資源集區](../administration/how-to-create-a-resource-pool.md)如需逐步指示。

## <a name="isolation-and-containment"></a>隔離和內含項目

處理架構已經過設計，以找出核心引擎處理從外部指令碼。 R 和 Python 指令碼執行以個別的處理序在本機的背景工作帳戶。 在 [工作管理員] 中，您可以監視 R 和 Python 處理程序，在低權限本機使用者帳戶，不同於 SQL Server 服務帳戶下執行。 

執行個別的低權限帳戶中的 R 和 Python 的處理程序有下列優點：

+ 隔離從 R 和 Python 工作階段，您可以終止 R 或 Python 處理程序，而不會影響核心資料庫作業的核心引擎處理序。 

+ 減少主機電腦上的外部指令碼執行階段處理程序的權限。

最低權限帳戶會在安裝期間建立，並放在 Windows*使用者帳戶集區*稱為**SQLRUserGroup**。 根據預設，此群組具有可執行檔、 程式庫和內建的資料集，使用 R 和 SQL Server 下的 Python 程式資料夾中的權限。 

擔任 DBA 一，您可以使用 SQL Server 資料安全性，來指定誰有權限來執行指令碼，並在相同的安全性角色來控制下管理作業中使用的資料存取透過 T-SQL 查詢。 身為系統管理員，您可以明確拒絕**SQLRUserGroup**藉由建立 Acl 的本機伺服器上的機密資料的存取權。

>[!NOTE]
> 根據預設， **SQLRUserGroup**不會在 SQL Server 本身不需要登入或權限。 背景工作帳戶應該進行資料存取需要登入，您必須建立它自己。 明確呼叫登入建立的案例是當使用者識別 Windows 使用者，而且連接字串會指定信任的使用者時，在執行中，資料或資料庫引擎執行個體上的作業支援從指令碼的要求。 如需詳細資訊，請參閱 <<c0> [ 為資料庫使用者的新增 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)。

## <a name="disable-script-execution"></a>停用指令碼執行

萬一失控的指令碼，您可以停用所有執行的指令碼，反轉之前如何將先啟用外部指令碼執行的步驟。

1. 在 SQL Server Management Studio 或其他查詢工具中，執行下列命令可設定`external scripts enabled`為 0 或 FALSE。

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. 重新啟動 database engine 服務。

一旦您解決此問題，請記得重新啟用執行個體上執行的指令碼，如果您想要繼續 R 和 Python 指令碼支援的 database engine 執行個體。 如需詳細資訊，請參閱[啟用指令碼執行](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>擴充功能

資料科學通常導入了封裝部署和管理新的需求。 資料科學家，對於常見的作法是利用自訂的解決方案中的開放原始碼和第三方封裝。 這些套件的一些會對其他套件相依性，在此情況下您可能需要評估，並安裝到您的目標的多個封裝。

負責伺服器資產的 DBA，作為部署到實際伺服器的任意 R 和 Python 套件表示不熟悉的挑戰。 然後再加入封裝，您應該評估是否外部的封裝所提供的功能是真正的必要項目，內建中沒有對等[R 語言](r-libraries-and-data-types.md)並[Python 程式庫](../python/python-libraries-and-data-types.md)安裝SQL Server 安裝程式。 

為伺服器封裝安裝的替代方案，資料科學家可能可以[建置，並在外部的工作站上執行解決方案](../r/set-up-a-data-science-client.md)，從 SQL Server 擷取資料，但使用所有分析本機上執行的工作站而不是在伺服器本身。 

如果您後來決定外部程式庫函式是的也不會造成伺服器作業或整個資料的風險，您可以選擇從多個方法來新增封裝。 在大部分情況下，系統管理員權限才能將套件新增至 SQL Server。 若要進一步了解，請參閱[SQL Server 中的安裝 Python 套件](../python/install-additional-python-packages-on-sql-server.md)並[SQL Server 中的安裝 R 封裝](install-additional-r-packages-on-sql-server.md)。

> [!NOTE]
> R 套件的伺服器管理員權限並不特別需要套件安裝如果您使用的替代方法。 請參閱[SQL Server 中的安裝 R 封裝](install-additional-r-packages-on-sql-server.md)如需詳細資訊。

## <a name="monitoring-script-execution"></a>監視指令碼執行

在中執行的 R 和 Python 指令碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]啟動[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]介面。 不過，[啟動列] 不是資源控管或分割區分開監視，因為它是適當方式管理資源的 Microsoft 所提供的安全服務。

使用管理在 Launchpad 服務下執行的外部指令碼[Windows 作業物件](/windows/desktop/ProcThread/job-objects)。 作業物件可讓您將處理序群組當作一個單位來管理。 每個作業物件都是階層式物件，並控制與其關聯之所有處理序的屬性。 在作業物件上執行的作業會影響與該作業物件關聯的所有處理序。

因此，如果您需要終止一個與某個物件關聯的作業，請注意，所有相關的處理序也將一併終止。 如果您正在執行指派給 Windows 作業物件的 R 指令碼，而該指令碼執行必須終止的相關 ODBC 作業，則父系 R 指令碼處理序也將一併終止。

如果您開始使用平行處理外部指令碼時，單一的 Windows 工作物件會管理所有平行子處理程序。

若要判斷處理序是否是在作業中執行，請使用 `IsProcessInJob` 函數。

## <a name="next-steps"></a>後續步驟

+ 檢閱的概念和元件[擴充性架構](../concepts/extensibility-framework.md)並[安全性](../concepts/security.md)更多的背景。

+ 您可能會在功能安裝，已經很熟悉使用者資料的存取控制，但如果沒有，請參閱[授與使用者權限，SQL Server machine learning](../security/user-permission.md)如需詳細資訊。 

+ 了解如何調整需要大量計算的機器學習服務工作負載的系統資源。 如需詳細資訊，請參閱 <<c0> [ 如何建立資源集區](../administration/how-to-create-a-resource-pool.md)。
