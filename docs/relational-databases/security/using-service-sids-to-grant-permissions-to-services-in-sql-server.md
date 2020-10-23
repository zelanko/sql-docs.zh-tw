---
description: 使用服務 SID 授與對 SQL Server 服務的權限
title: 使用服務 SID 授與服務的權限
ms.custom: seo-dt-2019
author: randomnote1
ms.author: dareist
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.openlocfilehash: ab9af4d073cbec00736bab6a24817502d353ffd8
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175928"
---
# <a name="using-service-sids-to-grant-permissions-to-services-in-sql-server"></a>使用服務 SID 授與對 SQL Server 服務的權限

SQL Server 會使用[個別服務安全性識別碼 (SID)](https://support.microsoft.com/help/2620201/sql-server-uses-a-service-sid-to-provide-service-isolation) (也稱為服務安全性主體 (SID)) 以允許直接對特定服務授與權限。 SQL Server 使用這個方法來授與對 SQL Server 引擎和代理程式服務的權限 (分別為 NT SERVICE\MSSQL$<InstanceName> 和 NT SERVICE\SQLAGENT$<InstanceName>)。 使用此方法，那些服務只能在服務正在執行時存取資料庫引擎。

授與對其他服務的權限時，也可以使用這個相同的方法。 使用服務 SID 可免除管理和維護服務帳戶的額外負荷，並針對授與對系統資源的權限，提供更緊密且更細微的控制。

可使用服務 SID 的服務範例如下：

- System Center Operations Manager 健全狀況服務 (NT SERVICE\HealthService)
- Windows Server 容錯移轉叢集 (WSFC) 服務 (NT SERVICE\ClusSvc)

某些服務預設沒有服務 SID。 必須使用 [SC.exe](/windows/desktop/services/configuring-a-service-using-sc) 建立服務 SID。 Microsoft System Center Operations Manager 系統管理員已採用[這個方法](https://kevinholman.com/2016/08/25/sql-mp-run-as-accounts-no-longer-required/)，授與對 SQL Server 內 HealthService 的權限。

一旦建立並確認服務 SID 之後，便必須在 SQL Server 中授與它權限。 授與權限是藉由使用 [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) 或查詢建立 Windows 登入而達成。 建立登入之後，便可以授與其權限、新增至角色，以及對應到資料庫，就像任何其他登入一樣。

> [!TIP]
> 如果收到 `Login failed for user 'NT AUTHORITY\SYSTEM'` 錯誤，請確認所需服務的服務 SID 存在、服務 SID 登入是在 SQL Server 中建立，且適當的權限已在 SQL Server 中授與給服務 SID。

## <a name="security"></a>安全性

### <a name="eliminate-service-accounts"></a>排除服務帳戶

傳統上服務帳戶一直用來允許服務登入 SQL Server。 服務帳戶增加一層額外的管理複雜度，因為必須維護和定期更新服務帳戶密碼。 此外，個人嘗試在執行個體中執行動作時，也可能用服務帳戶認證來遮掩其活動。

### <a name="granular-permissions-to-system-accounts"></a>細微的系統帳戶權限

系統帳戶在過去是藉由為 [LocalSystem](/windows/win32/services/localsystem-account) ([en-us 的 NT AUTHORITY\SYSTEM](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Localized_service_names)) 或[NetworkService](/windows/desktop/Services/networkservice-account) ([en-us 的 NT AUTHORITY\NETWORK SERVICE](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Localized_service_names)) 帳戶建立登入並授與這些登入權限而獲得授與權限。 這個方法會授與任何處理序或服務對以系統帳戶執行的 SQL 權限。

使用服務 SID，可容許授與對特定服務的權限。 服務只有在執行時，才能存取它已獲得授與權限的資源。 例如，如果 `HealthService` 以 `LocalSystem` 身分執行，且獲得授與 `View Server State`，則 `LocalSystem` 帳戶只有在 `HealthService` 的內容中執行時才具有 `View Server State` 的權限。 如果任何其他處理序嘗試以 `LocalSystem` 身分存取 SQL 的伺服器狀態，它們將會遭到拒絕存取。

## <a name="examples"></a>範例

### <a name="a-create-a-service-sid"></a>A. 建立服務 SID

下列 PowerShell 命令會在 System Center Operations Manager 健全狀況服務上建立服務 SID。

```PowerShell
sc.exe --% sidtype "HealthService" unrestricted
```

> [!IMPORTANT]
> `--%` 會告知 PowerShell 停止剖析命令的其餘部分。 使用舊版命令和應用程式時，這非常有用。

### <a name="b-query-a-service-sid"></a>B. 查詢服務 SID

若要檢查服務 SID，或確保服務 SID 已存在，請在 PowerShell 中執行下列命令。

```PowerShell
sc.exe --% qsidtype "HealthService"
```

> [!IMPORTANT]
> `--%` 會告知 PowerShell 停止剖析命令的其餘部分。 使用舊版命令和應用程式時，這非常有用。

### <a name="c-add-a-newly-created-service-sid-as-a-login"></a>C. 新增剛建立的服務 SID 作為登入

下列範例會使用 T-SQL 建立 System Center Operations Manager 健全狀況服務的登入。

```SQL
CREATE LOGIN [NT SERVICE\HealthService] FROM WINDOWS
GO
```

### <a name="d-add-an-existing-service-sid-as-a-login"></a>D. 新增現有的服務 SID 作為登入

下列範例會使用 T-SQL 建立叢集服務的登入。 直接授與叢集服務權限，就不需要授與過多的權限給 SYSTEM 帳戶。

```SQL
CREATE LOGIN [NT SERVICE\ClusSvc] FROM WINDOWS
GO
```

### <a name="e-grant-permissions-to-a-service-sid"></a>E. 將權限授與服務 SID

授與叢集服務管理可用性群組所需的權限。

```SQL
GRANT ALTER ANY AVAILABILITY GROUP TO [NT SERVICE\ClusSvc]
GO

GRANT CONNECT SQL TO [NT SERVICE\ClusSvc]
GO

GRANT VIEW SERVER STATE TO [NT SERVICE\ClusSvc]
GO
```

  > [!NOTE]
  > 移除服務 SID 登入或是從 sysadmin 伺服器角色加以移除，可能會導致 SQL Server 會連線至 SQL Server 資料庫引擎的各種元件發生問題。 部分問題如下：
  > - SQL Server Agent 無法啟動或連線至 SQL Server 服務
  > - SQL Server 安裝程式遇到下列 Microsoft 知識庫文章中所述的問題： https://support.microsoft.com/help/955813/you-may-be-unable-to-restart-the-sql-server-agent-service-after-you-re \(英文\)
  >
  > 針對 SQL Server 的預設執行個體，您可以透過使用下列 Transact-SQL 命令來新增服務 SID 以修正此情況：
  >
  > ```sql
  > CREATE LOGIN [NT SERVICE\MSSQLSERVER] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\MSSQLSERVER]
  > 
  > CREATE LOGIN [NT SERVICE\SQLSERVERAGENT] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\SQLSERVERAGENT]
  > ```
  > 針對 SQL Server 的具名執行個體，請使用下列 Transact-SQL 命令：
  > ```sql
  > CREATE LOGIN [NT SERVICE\MSSQL$SQL2019] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\MSSQL$SQL2019]
  > 
  > CREATE LOGIN [NT SERVICE\SQLAgent$SQL2019] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
  > 
  > ALTER ROLE sysadmin ADD MEMBER [NT SERVICE\SQLAgent$SQL2019]
  > 
  > ```
  > 在此範例中，`SQL2019` 是 SQL Server 的執行個體名稱。

## <a name="next-steps"></a>後續步驟

如需服務 SID 結構的詳細資訊，請閱讀 [SERVICE_SID_INFO 結構](/windows/win32/api/winsvc/ns-winsvc-service_sid_info)。

了解[建立登入](../../t-sql/statements/create-login-transact-sql.md)時可用的其他選項。

若要使用角色型安全性搭配服務 SID，請參閱 SQL Server 中的[建立角色](../../t-sql/statements/create-role-transact-sql.md)。

了解使用服務 SID [授與對 SQL Server 服務的權限](../../t-sql/statements/grant-transact-sql.md)。
