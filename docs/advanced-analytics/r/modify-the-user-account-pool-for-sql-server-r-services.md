---
title: "修改 SQL Server R Services 的使用者帳戶集區 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33e22f7edec807d046798d89a9cd5daa642e8d3b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="modify-the-user-account-pool-for-sql-server-r-services"></a>修改 SQL Server R Services 的使用者帳戶集區
  在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安裝程序中，會建立新的 Windows「使用者帳戶集區」，以支援 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的執行作業。 這些工作者帳戶的目的是針對不同 SQL 使用者同時執行 R 指令碼來進行隔離。 

本主題描述預設設定、工作者帳戶的安全性和功能，以及如何變更預設設定。

## <a name="worker-accounts-used-by-r-services"></a>R Services 使用的工作者帳戶   

Windows 帳戶群組是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式針對已安裝 R Services 的每個執行個體所建立。 因此，如果您安裝了多個支援 R 的執行個體，就會有多個使用者群組。

-   在預設的執行個體中，群組名稱是 **SQLRUserGroup**。 
-   在具名的執行個體中，預設群組名稱的最後會加上執行個體名稱：例如，**SQLRUserGroupMyInstanceName**。 

根據預設，使用者帳戶集區包含 20 個使用者帳戶。 在大部分情況下，20 個已足夠支援 R 工作階段，但您可以變更帳戶的數量。
-  在預設的執行個體中，個別的帳戶會命名為 **MSSQLSERVER01** 到 **MSSQLSERVER20**。  
-   對於具名的執行個體，個別的帳戶會以執行個體的名稱來命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。  

### <a name = "HowToChangeGroup"> </a>如何變更 R 工作者帳戶的數目

若要修改帳戶集區中的使用者數目，請依照下列說明，編輯 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務的屬性。  
  
每個使用者帳戶相關聯的密碼都是隨機產生的，但您可以在帳戶建立之後變更密碼。  
  
1. 開啟 [SQL Server 組態管理員]，並選取 [SQL Server 服務]。
2. 按兩下 SQL Server Launchpad 服務，如果服務正在執行請將它停止。 
3.  在 [服務] 索引標籤上，請確定 [啟動模式] 設為 [自動]。 如果 Launchpad 未執行，則 R 指令碼會失敗。
4.  按一下 [進階] 索引標籤，並視需要編輯 [外部使用者計數] 的值。 這個設定會控制使用 R 同時執行查詢的不同 SQL 使用者數量。預設為 20 個帳戶。
5. 如果您的組織要求定期變更密碼，您可以選擇將 [重設外部使用者密碼] 選項設為 [是]。 如此會重新產生 Launchpad 為使用者帳戶維護的加密密碼。 如需詳細資訊，請參閱[強制密碼原則](#bkmk_EnforcePolicy)。    
6.  重新啟動服務。  

## <a name="managing-r-workload"></a>管理 R 工作負載

這個集區的帳戶數目會決定可以同時啟用多少個 R 工作階段。  根據預設，系統會建立 20 帳戶，表示可以同時有 20 個不同的使用者具有使用中的 R 工作階段。 如果您預期會有更多使用者同時執行 R 指令碼的需要，則可以增加工作者帳戶的數目。 

當同一個使用者同時執行多個 R 指令碼時，該使用者執行的所有工作階段都會使用相同的工作者帳戶。 例如，若資源允許，單一使用者可能使用單一工作者帳戶，同時執行 100 個不同的 R 指令碼。

您可以支援的工作者帳戶數目，以及任何單一使用者可同時執行的 R 工作階段數目，都只受限於伺服器資源。  一般而言，使用 R 執行階段時，記憶體將會是您遇到的第一個瓶頸。

在 R Services 中，R 指令碼可以使用的資源是由 SQL Server 管理。 建議您使用 SQL Server DMV 來監視資源使用狀況，或是查看 Windows 工作物件相關的效能計數器，並隨之調整伺服器記憶體的使用。 
 
如果您使用 SQL Server Enterprise Edition，則可以設定[外部資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)，以配置用於執行 R 指令碼的資源。 

如需管理 R 指令碼功能的詳細資訊，請參閱下列文章：

- [適用於 R Services 的 SQL Server 組態](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
-  [R Services 的效能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)

## <a name="security"></a>安全性

每個使用者群組都與特定執行個體上的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務相關聯，且不支援在其他執行個體上執行的 R 作業。

對於每個工作者帳戶，當工作階段在作用中時，系統會建立一個暫存資料夾來儲存指令碼物件、中繼結果，以及在 R 指令碼執行期間 R 和 SQL Server 所使用的其他資訊。 只有系統管理員可以存取這些位於 ExtensibilityData 資料夾之下的工作檔案，且 SQL Server 會在指令碼完成之後清除這些工作檔案。 

如需詳細資訊，請參閱[安全性概觀](../../advanced-analytics/r-services/security-overview-sql-server-r.md)。

### <a name="bkmk_EnforcePolicy"></a>強制執行密碼原則

如果您的組織要求定期變更密碼，您可能需要強制 Launchpad 服務重新產生為其工作者帳戶維護的加密密碼。  

若要啟用此設定並強制密碼重新整理，請在 SQL Server 組態管理員中開啟 Launchpad 服務的 [屬性] 窗格，按一下 [進階]，然後將 [重設外部使用者密碼] 變更為 [是]。 當您套用此變更時，系統會立即針對所有使用者帳戶重新產生密碼。 若要在此變更之後使用 R 指令碼，您必須重新啟動 Launchpad 服務，它就會讀取新產生的密碼。 

若要定期重設密碼，您可以手動設定此旗標，或使用指令碼。

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>支援遠端計算內容所需的其他必要權限

根據預設，R 工作者帳戶群組沒有相關聯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的登入權限。 如果任何 R 使用者從遠端用戶端連線到 SQL Server 以執行 R 指令碼，或如果指令碼使用 ODBC 來取得其他資料，就可能會造成問題。 

若要確認可支援這些案例，資料庫系統管理員必須提供 R 工作者帳戶群組權限，以登入 R 指令碼將在其上執行的 SQL Server 執行個體 ([連線到] 權限)。 這稱為「隱含驗證」，可讓 SQL Server 使用遠端使用者的認證來執行 R 指令碼。

> [!NOTE]
> 如果您使用 SQL 登入從遠端工作站執行 R 指令碼，即不適用這項限制，因為 SQL 登入認證會明確地從 R 用戶端傳遞至 SQL Server 執行個體，再傳到 ODBC。


### <a name="how-to-enable-implied-authentication"></a>如何啟用隱含驗證

1. 在您要執行 R 程式碼的執行個體上，以系統管理員身分來開啟 SQL Server Management Studio。

2. 執行下列指令碼。 如果已變更預設值，以及電腦和執行個體名稱，請務必編輯使用者群組名稱。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ````


  
## <a name="see-also"></a>另請參閱  
 [組態 (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  

