---
title: 設定平行或並行執行 R 和 Python 指令碼
description: 在使用者帳戶集區中設定平行或並行執行 R 和 Python 指令碼，以調整 SQL Server Machine Learning 服務。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/25/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 525e9d0931b3ff25d4258004680ed158a9baf82d
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484430"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>在 SQL Server Machine Learning 服務中調整外部指令碼的平行執行
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

深入了解 SQL Server Machine Learning 服務的工作角色帳戶，以及如何變更預設設定，以調整外部指令碼的平行執行數目。

在 Machine Learning 服務的安裝過程中，會建立新的 Windows 使用者帳戶集區  ，以支援 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務執行工作。 這些工作者帳戶的目的是針對不同 SQL Server 使用者同時執行外部指令碼來進行隔離。

> [!Note]
> 在 SQL Server 2019 中，**SQLRUserGroup** 只有一個成員，且現在是單一 SQL Server Launchpad 服務帳戶，而不是多個背景工作角色帳戶。 本文說明 SQL Server 2016 和 2017 的背景工作帳戶。

## <a name="worker-account-group"></a>背景工作帳戶群組

針對安裝並啟用機器學習的每個執行個體，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式都會建立一個 Windows 帳戶群組。

- 在預設的執行個體中，群組名稱是 **SQLRUserGroup**。 無論您使用的是 Python 或 R 或兩者，名稱都相同。
- 在具名的執行個體中，預設群組名稱的最後會加上執行個體名稱：例如，**SQLRUserGroupMyInstanceName**。

根據預設，使用者帳戶集區包含 20 個使用者帳戶。 在大部分情況下，20 個已足夠支援機器學習工作，但您可以變更帳戶的數量。 帳戶數的上限為 100。

- 在預設的執行個體中，個別的帳戶會命名為 **MSSQLSERVER01** 到 **MSSQLSERVER20**。
- 對於具名的執行個體，個別的帳戶會以執行個體的名稱來命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。

如果有一個以上的執行個體使用機器學習，電腦將會有多個使用者群組。 群組無法跨執行個體共用。

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>背景工作帳戶的數目

若要修改帳戶集區中的使用者數目，請依照下列說明，編輯 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的屬性。

每個使用者帳戶相關聯的密碼都是隨機產生的，但您可以在帳戶建立之後變更密碼。

1. 開啟 [SQL Server 組態管理員]，並選取 [SQL Server 服務]  。
2. 按兩下 SQL Server Launchpad 服務，如果服務正在執行請將它停止。
3.  在 [服務]  索引標籤上，請確定 [啟動模式] 設為 [自動]。 當 Launchpad 未執行時，外部指令碼無法啟動。
4.  按一下 [進階]  索引標籤，並視需要編輯 [外部使用者計數]  的值。 此設定會控制有多少不同的 SQL 使用者可以同時執行外部指令碼工作階段。 預設為 20 個帳戶。 使用者數目上限為 100。
5. 如果您的組織要求定期變更密碼，您可以選擇將 [重設外部使用者密碼]  選項設為 [是]  。 如此會重新產生 Launchpad 為使用者帳戶維護的加密密碼。 如需詳細資訊，請參閱[強制密碼原則](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy)。
6.  重新啟動 Launchpad 服務。

## <a name="managing-workloads"></a>管理工作負載

這個集區的帳戶數目會決定可以同時啟用多少個外部指令碼工作階段。  根據預設，系統會建立 20 個帳戶，表示可以同時有 20 個不同的使用者具有使用中的 Python 或 R 工作階段。 如果您預期會執行 20 個以上的並行指令碼，則可以增加背景工作帳戶的數目。

當同一個使用者同時執行多個外部指令碼時，該使用者執行的所有工作階段都會使用相同的背景工作帳戶。 例如，只要資源允許，單一使用者可能會有 100 個不同的 Python 或 R 指令碼同時執行，但是所有指令碼都是使用單一背景工作帳戶來執行。

您可以支援的工作者帳戶數目，以及任何單一使用者可同時執行的工作階段數目，都只受限於伺服器資源。 一般而言，使用 Python 或 R 執行階段時，記憶體將會是您遇到的第一個瓶頸。

Python 或 R 指令碼可以使用的資源是由 SQL Server 管理。 建議您使用 SQL Server DMV 來監視資源使用狀況，或是查看 Windows 工作物件相關的效能計數器，並隨之調整伺服器記憶體的使用。 如果您使用 SQL Server Enterprise Edition，則可以設定[外部資源集區](create-external-resource-pool.md)，以配置用於執行外部指令碼的資源。

## <a name="next-steps"></a>後續步驟

- [使用 SQL Server Management Studio 中的自訂報表監視 Python 與 R 指令碼執行](../../machine-learning/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [使用動態管理檢視 (DMV) 監視 SQL Server 機器學習服務](../../machine-learning/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)