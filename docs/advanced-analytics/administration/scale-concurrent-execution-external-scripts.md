---
title: 擴充外部腳本的並存執行
description: 在使用者帳戶集區中設定平行或並行 R 和 Python 腳本執行, 以調整 SQL Server Machine Learning 服務。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 262810be3ad1fd246c6f60383e28d456c6b79e08
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714332"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>在 SQL Server Machine Learning 服務中調整外部腳本的並存執行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

瞭解 SQL Server Machine Learning 服務的背景工作帳戶，以及如何變更預設設定，以調整外部腳本的並存執行數目。

在 Machine Learning 服務的安裝過程中，會建立新的 Windows*使用者帳戶集*區，以支援 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務執行工作。 這些背景工作帳戶的目的是要以不同的 SQL Server 使用者隔離外部腳本的並存執行。

> [!Note]
> 在 SQL Server 2019 中, **SQLRUserGroup**只有一個成員, 現在是單一 SQL Server Launchpad 服務帳戶, 而不是多個背景工作帳戶。 本文說明 SQL Server 2016 和2017的背景工作帳戶。

## <a name="worker-account-group"></a>背景工作帳戶群組

安裝並啟用機器學習服務的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]每個實例, 都會建立一個 Windows 帳戶群組。

- 在預設的執行個體中，群組名稱是 **SQLRUserGroup**。 無論您使用的是 Python 或 R 或兩者，名稱都相同。
- 在具名的執行個體中，預設群組名稱的最後會加上執行個體名稱：例如，**SQLRUserGroupMyInstanceName**。

根據預設，使用者帳戶集區包含 20 個使用者帳戶。 在大部分情況下, 20 比支援機器學習工作所需的還多, 但是您可以變更帳戶數目。 帳戶數目上限為100。

- 在預設的執行個體中，個別的帳戶會命名為 **MSSQLSERVER01** 到 **MSSQLSERVER20**。
- 對於具名的執行個體，個別的帳戶會以執行個體的名稱來命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。

如果有一個以上的實例使用機器學習, 電腦將會有多個使用者群組。 群組無法在實例之間共用。

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>背景工作帳戶數目

若要修改帳戶集區中的使用者數目，請依照下列說明，編輯 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的屬性。

每個使用者帳戶相關聯的密碼都是隨機產生的，但您可以在帳戶建立之後變更密碼。

1. 開啟 [SQL Server 組態管理員]，並選取 [SQL Server 服務]。
2. 按兩下 SQL Server Launchpad 服務，如果服務正在執行請將它停止。
3.  在 [服務] 索引標籤上，請確定 [啟動模式] 設為 [自動]。 當啟動列未執行時, 外部腳本無法啟動。
4.  按一下 [進階] 索引標籤，並視需要編輯 [外部使用者計數] 的值。 此設定會控制有多少不同的 SQL 使用者可以同時執行外部腳本會話。 預設值為20個帳戶。 使用者數目上限為100。
5. 如果您的組織要求定期變更密碼，您可以選擇將 [重設外部使用者密碼] 選項設為 [是]。 如此會重新產生 Launchpad 為使用者帳戶維護的加密密碼。 如需詳細資訊，請參閱[強制密碼原則](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy)。
6.  重新開機啟動列服務。

## <a name="managing-workloads"></a>管理工作負載

此集區中的帳戶數目會決定可以同時啟用多少個外部腳本會話。  根據預設，系統會建立20個帳戶，這表示20個不同的使用者一次可以有作用中的 Python 或 R 會話。 如果您預期會執行20個以上的並行腳本, 則可以增加背景工作帳戶的數目。

當相同使用者同時執行多個外部腳本時, 該使用者所執行的所有會話都會使用相同的背景工作帳戶。 例如，如果資源允許，單一使用者可能會有100個不同的 Python 或 R 腳本同時執行，但所有腳本都是使用單一背景工作帳戶來執行。

您可以支援的背景工作帳戶數目, 以及任何單一使用者可以執行的並行會話數目, 只受限於伺服器資源。 一般而言，記憶體是您在使用 Python 或 R 執行時間時會遇到的第一個瓶頸。

Python 或 R 腳本可以使用的資源是由 SQL Server 所控制。 建議您使用 SQL Server DMV 來監視資源使用狀況，或是查看 Windows 工作物件相關的效能計數器，並隨之調整伺服器記憶體的使用。 如果您有 SQL Server Enterprise Edition, 您可以藉由設定[外部資源集](how-to-create-a-resource-pool.md)區來配置用來執行外部腳本的資源。

## <a name="next-steps"></a>後續步驟

- [使用 SQL Server Management Studio 中的自訂報表監視 Python 和 R 腳本執行](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [使用動態管理檢視（Dmv）監視 SQL Server Machine Learning 服務](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)