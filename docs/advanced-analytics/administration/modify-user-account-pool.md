---
title: 在 SQL Server Machine Learning 服務調整並行執行外部指令碼 |Microsoft Docs
description: 如何修改使用者帳戶集區擴充 SQL Server Machine Learning 服務。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 598c303d6b0e3ef334ddb9b03d2c5d9c21401395
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2018
ms.locfileid: "48881397"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>小數位數的同時執行的 SQL Server Machine Learning 服務中的外部指令碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 安裝程序中，會建立新的 Windows「使用者帳戶集區」，以支援 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的執行作業。 這些工作者帳戶的目的是要隔離並行執行由不同的 SQL 使用者的外部指令碼。

這篇文章描述的預設組態和容量的背景工作帳戶，以及如何變更預設組態，以在 SQL Server Machine Learning 服務來調整的同時執行外部指令碼的數目。

**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]， [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="worker-account-group"></a>背景工作帳戶群組

Windows 帳戶群組由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]machine learning 會安裝並啟用每個執行個體的安裝程式。

- 在預設的執行個體中，群組名稱是 **SQLRUserGroup**。 不論您是使用 R 或 Python 或兩者的名稱都是一樣的。
- 在具名的執行個體中，預設群組名稱的最後會加上執行個體名稱：例如，**SQLRUserGroupMyInstanceName**。

根據預設，使用者帳戶集區包含 20 個使用者帳戶。 在大部分情況下，20 個已足夠支援機器學習工作，但您可以變更帳戶的數目。 帳戶的數目上限為 100。

- 在預設的執行個體中，個別的帳戶會命名為 **MSSQLSERVER01** 到 **MSSQLSERVER20**。
- 對於具名的執行個體，個別的帳戶會以執行個體的名稱來命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。

如果多個執行個體使用機器學習服務，電腦會有多個使用者群組。 群組不能執行個體之間共用。

> [!Note]
> 在 SQL Server 2019， **SQLRUserGroup**只有一個成員現在是單一的 SQL Server Launchpad 服務帳戶，而不是多個背景工作帳戶。

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>背景工作帳戶數目

若要修改帳戶集區中的使用者數目，請依照下列說明，編輯 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的屬性。

每個使用者帳戶相關聯的密碼都是隨機產生的，但您可以在帳戶建立之後變更密碼。

1. 開啟 [SQL Server 組態管理員]，並選取 [SQL Server 服務]。
2. 按兩下 SQL Server Launchpad 服務，如果服務正在執行請將它停止。
3.  在 [服務] 索引標籤上，請確定 [啟動模式] 設為 [自動]。 Launchpad 未執行時，無法啟動外部指令碼。
4.  按一下 [進階] 索引標籤，並視需要編輯 [外部使用者計數] 的值。 此設定控制多少不同的 SQL 使用者可以執行外部指令碼同時工作階段。 預設為 20 個帳戶。 使用者數目上限為 100。
5. 如果您的組織要求定期變更密碼，您可以選擇將 [重設外部使用者密碼] 選項設為 [是]。 如此會重新產生 Launchpad 為使用者帳戶維護的加密密碼。 如需詳細資訊，請參閱[強制密碼原則](#bkmk_EnforcePolicy)。
6.  重新啟動 Launchpad 服務。

## <a name="managing-workloads"></a>管理工作負載

此集區的帳戶數目會決定多少個外部指令碼工作階段可以同時啟用。  根據預設，會建立 20 帳戶，這表示可以有 20 個不同的使用者使用 R 或 Python 中工作階段一次。 如果您預期要執行超過 20 個並行的指令碼，您可以增加工作者帳戶數目。

當同一個使用者同時執行多個外部指令碼時，所有由該使用者所執行的工作階段會使用相同的背景工作帳戶。 例如，單一使用者可能有 100 不同的 R 指令碼同時執行，只要資源允許，但所有指令碼會使用單一背景工作帳戶來執行。

背景工作帳戶，您可以支援的數目和任何單一使用者可以執行，並行工作階段的數目是只受限於伺服器資源。 一般而言，使用 R 執行階段時，記憶體將會是您遇到的第一個瓶頸。

SQL Server 所控管可供 Python 或 R 指令碼的資源。 建議您使用 SQL Server DMV 來監視資源使用狀況，或是查看 Windows 工作物件相關的效能計數器，並隨之調整伺服器記憶體的使用。 如果您有 SQL Server Enterprise Edition 時，您可以配置用來執行外部指令碼所設定的資源[外部資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)。

如需有關管理機器學習工作的容量，請參閱下列文章：

- [R services 的 SQL Server 組態](../../advanced-analytics/r/sql-server-configuration-r-services.md)
- [R Services 的效能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)