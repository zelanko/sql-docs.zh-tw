---
title: 修改 SQL Server 機器學習的使用者帳戶集區 |Microsoft 文件
ms.date: 11/03/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 7c1efa87fef881a8b88b0967716ec062cf95e64f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="modify-the-user-account-pool-for-sql-server-machine-learning"></a>修改 SQL Server 機器學習的使用者帳戶集區
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 安裝程序中，會建立新的 Windows「使用者帳戶集區」，以支援 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的執行作業。 這些工作者帳戶的用途是將隔離同時執行的不同的 SQL 使用者的外部指令碼。

本文說明的預設組態、 安全性和產能的背景工作帳戶，以及如何變更預設組態。

**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]， [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="worker-accounts-used-for-external-script-execution"></a>用於外部指令碼執行的背景工作帳戶

Windows 帳戶群組由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]machine learning 已安裝並啟用每個執行個體的安裝程式。

-   在預設的執行個體中，群組名稱是 **SQLRUserGroup**。 不論您使用 R、 Python 或兩者的名稱都是相同的。
-   在具名的執行個體中，預設群組名稱的最後會加上執行個體名稱：例如，**SQLRUserGroupMyInstanceName**。

根據預設，使用者帳戶集區包含 20 個使用者帳戶。 在大部分情況下，20 足以多個支援機器學習工作，但您可以變更帳戶的數目。
-  在預設的執行個體中，個別的帳戶會命名為 **MSSQLSERVER01** 到 **MSSQLSERVER20**。
-   對於具名的執行個體，個別的帳戶會以執行個體的名稱來命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。

如果多個執行個體使用機器學習，電腦會有多個使用者群組。 群組不能在執行個體之間共用。

### <a name = "HowToChangeGroup"> </a>如何變更的背景工作帳戶數目

若要修改帳戶集區中的使用者數目，請依照下列說明，編輯 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的屬性。

每個使用者帳戶相關聯的密碼都是隨機產生的，但您可以在帳戶建立之後變更密碼。

1. 開啟 [SQL Server 組態管理員]，並選取 [SQL Server 服務]。
2. 按兩下 SQL Server Launchpad 服務，如果服務正在執行請將它停止。
3.  在 [服務] 索引標籤上，請確定 [啟動模式] 設為 [自動]。 未執行 [啟動列] 時，無法啟動外部指令碼。
4.  按一下 [進階] 索引標籤，並視需要編輯 [外部使用者計數] 的值。 這個設定會控制多少不同的 SQL 使用者可以執行外部指令碼工作階段同時。 預設為 20 個帳戶。
5. 如果您的組織要求定期變更密碼，您可以選擇將 [重設外部使用者密碼] 選項設為 [是]。 如此會重新產生 Launchpad 為使用者帳戶維護的加密密碼。 如需詳細資訊，請參閱[強制密碼原則](#bkmk_EnforcePolicy)。
6.  重新啟動 [啟動列] 服務。

## <a name="managing-machine-learning-workloads"></a>管理機器學習工作負載

在此集區帳戶數目決定多少個外部指令碼工作階段可以同時啟用。  根據預設，會建立 20 個帳戶，這表示 20 個不同的使用者可以有作用中 R 或 Python 工作階段一次。 如果您預期執行超過 20 個並行的指令碼，您可以增加背景工作帳戶數目。

當相同的使用者同時執行多個外部指令碼時，所有由該使用者所執行的工作階段會使用相同的背景工作帳戶。 例如，單一使用者可能會有 100 不同 R 指令碼同時執行，只要允許資源，但所有的指令碼會使用單一的背景工作帳戶執行。

背景工作帳戶，可以支援的數目和可執行的任何單一使用者，並行工作階段數目受限於只能由伺服器資源。 一般而言，使用 R 執行階段時，記憶體將會是您遇到的第一個瓶頸。

SQL Server 所控管可以由 Python 或 R 指令碼中使用的資源。 建議您使用 SQL Server DMV 來監視資源使用狀況，或是查看 Windows 工作物件相關的效能計數器，並隨之調整伺服器記憶體的使用。 如果您有 SQL Server Enterprise Edition 時，您可以配置資源用來執行外部指令碼，藉由設定[外部資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)。

如需有關管理機器學習工作的容量，請參閱下列文章：

- [R Services 的 SQL Server 組態](../../advanced-analytics/r/sql-server-configuration-r-services.md)
-  [R 服務的效能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)

## <a name="security"></a>Security

每個使用者群組都與特定執行個體上的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務相關聯，且不支援在其他執行個體上執行的 R 作業。

對於每個工作者帳戶，當工作階段在作用中時，系統會建立一個暫存資料夾來儲存指令碼物件、中繼結果，以及在 R 指令碼執行期間 R 和 SQL Server 所使用的其他資訊。 只有系統管理員可以存取這些位於 ExtensibilityData 資料夾之下的工作檔案，且 SQL Server 會在指令碼完成之後清除這些工作檔案。 

如需詳細資訊，請參閱[安全性概觀](../../advanced-analytics/r-services/security-overview-sql-server-r.md)。

### <a name="bkmk_EnforcePolicy"></a>強制執行密碼原則

如果您的組織要求定期變更密碼，您可能需要強制 Launchpad 服務重新產生為其工作者帳戶維護的加密密碼。  

若要啟用此設定並強制密碼重新整理，請在 SQL Server 組態管理員中開啟 Launchpad 服務的 [屬性] 窗格，按一下 [進階]，然後將 [重設外部使用者密碼] 變更為 [是]。 當您套用此變更時，系統會立即針對所有使用者帳戶重新產生密碼。 若要在此變更之後使用 R 指令碼，您必須重新啟動 Launchpad 服務，它就會讀取新產生的密碼。 

若要定期重設密碼，您可以手動設定此旗標，或使用指令碼。

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>支援遠端計算內容所需的其他必要權限

根據預設，R 工作者帳戶群組沒有相關聯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的登入權限。 如果任何 R 使用者從遠端用戶端連線到 SQL Server 以執行 R 指令碼，或如果指令碼使用 ODBC 來取得其他資料，就可能會造成問題。 

若要確認可支援這些案例，資料庫系統管理員必須提供 R 工作者帳戶群組權限，以登入 R 指令碼將在其上執行的 SQL Server 執行個體 ([連線到] 權限)。 這指*隱含的驗證*，並可讓 SQL Server 執行 R 指令碼，使用遠端使用者的認證。

> [!NOTE]
> 如果您使用 SQL 登入從遠端工作站執行 R 指令碼，即不適用這項限制，因為 SQL 登入認證會明確地從 R 用戶端傳遞至 SQL Server 執行個體，再傳到 ODBC。


### <a name="how-to-enable-implied-authentication"></a>如何啟用隱含驗證

1. 您將在其中執行 R 或 Python 程式碼的執行個體上系統管理員身分開啟 SQL Server Management Studio。

2. 執行下列指令碼。 如果已變更預設值，以及電腦和執行個體名稱，請務必編輯使用者群組名稱。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ````

