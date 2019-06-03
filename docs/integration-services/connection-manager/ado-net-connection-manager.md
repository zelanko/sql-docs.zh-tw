---
title: ADO.NET 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bee4d3ea71aaeacf682a6e90fad91786fa7a0c9c
ms.sourcegitcommit: e92ce0f59345fe61c0dd3bfe495ef4b1de469d4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/25/2019
ms.locfileid: "66221178"
---
# <a name="adonet-connection-manager"></a>ADO.NET 連接管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員可讓封裝使用 .NET 提供者來存取資料來源。 此連線管理員通常用於存取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這類的資料來源，以及透過自訂工作 (使用如 C# 這類語言以 Managed 程式碼撰寫) 中之 OLE DB 和 XML 公開的資料來源。  
  
 當您將 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員加入封裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立一個連線管理員 (在執行階段會解析為 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接)、設定連線管理員屬性，並將該連線管理員加入封裝上的 **Connections** 集合。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 **ADO.NET**。 系統會限定 **ConnectionManagerType** 的值，以包含連線管理員使用之 .NET 提供者的名稱。  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 連接管理員疑難排解  
 您可以記錄 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員對外部資料來源執行的連接。 若要記錄 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷]  事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 由 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員讀取時，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期資料類型的資料將會產生如下表所示的結果。  
  
|SQL Server 資料類型|結果|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|除非封裝使用參數化 SQL 命令，否則封裝會失敗。 若要使用參數化 SQL 命令，請在封裝中使用「執行 SQL 工作」。 如需詳細資訊，請參閱 [執行 SQL 工作](../../integration-services/control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)。|  
|**datetime2**|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員會截斷毫秒值。|  
  
> [!NOTE]  
>  如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型以及如何將其對應到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) 和 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="adonet-connection-manager-configuration"></a>ADO.NET 連接管理員組態  
 您可以利用下列方式設定 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員：  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
-   提供設定的特定連接字串，以符合所選 .NET 提供者的需求。  
  
-   視提供者而定，包含要連接的資料來源名稱。  
  
-   為所選的提供者提供適當的安全性認證。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員的許多組態選項依存於連線管理員使用的 .NET 提供者。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定 ADO.NET 連接管理員](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="configure-adonet-connection-manager"></a>設定 ADO.NET 連接管理員
  使用 [設定 ADO.NET 連線管理員]  對話方塊加入資料來源的連接，可使用 .NET Framework 資料提供者 (例如 SqlClient 提供者) 來存取此資料來源。 連接管理員可以使用現有的連接，或者您也可以建立新的連接。  
  
 若要深入了解 ADO.NET 連線管理員，請參閱 [ADO.NET 連線管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **資料連接**  
 從清單中選取現有的 ADO.NET 資料連接。  
  
 **資料連接屬性**  
 檢視選取之 ADO.NET 資料連接的屬性和值。  
  
 **新增**  
 使用 [連線管理員]  對話方塊來建立 ADO.NET 資料連接。  
  
 **刪除**  
 請選取一個連接，然後使用 [刪除]  按鈕刪除它。  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Azure 資源驗證的受控識別
在 [Azure Data Factory 中的 Azure-SSIS 整合執行階段](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)上執行 SSIS 套件時，您可以使用與您資料處理站建立關聯的[受控識別](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity)來進行 Azure SQL Database (或受控執行個體) 驗證。 指定的處理站可以使用此身分識別從您資料庫存取資料，或從您的資料庫複製資料。

若要使用 Azure SQL Database 的受控識別驗證，請遵循下列步驟來設定您的資料庫：

1. **在 Azure AD 中建立群組。** 將受控識別新增為群組的成員。
    
   1. [從 Azure 入口網站尋找資料處理站受控識別](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)。 前往您資料處理站的**屬性**。 複製**受控識別物件識別碼**。
    
   1. 安裝 [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) 模組。 使用 `Connect-AzureAD` 命令登入。 執行下列命令來建立群組，並將受控識別新增為成員。
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. 在 Azure 入口網站為您的 Azure SQL Server **[佈建 Azure Active Directory 系統管理員](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** ，如果您尚未這麼做。 Azure AD 系統管理員可以是 Azure AD 使用者或 Azure AD 群組。 如果您授與受控識別系統管理員角色，請略過步驟 3 和 4。 系統管理員將擁有資料庫的完整存取權。

1. 為 Azure AD 群組 **[建立自主資料庫使用者](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** 。 使用至少具有 ALTER ANY USER 權限的 Azure AD 身分識別，使用 SSMS 等工具連線至您要複製資料的資料庫。 執行下列 T-SQL： 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. 依照您平常為 SQL 使用者和其他人所進行的操作一樣**授與 Azure AD 群組所需權限**。 例如，執行下列程式碼：

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

若要使用 Azure SQL Database 受控執行個體的受控識別驗證，請遵循下列步驟來設定您的資料庫：
    
1. 在 Azure 入口網站為您的受控執行個體 **[佈建 Azure Active Directory 系統管理員](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)** ，如果您尚未這麼做。 Azure AD 系統管理員可以是 Azure AD 使用者或 Azure AD 群組。 如果您授與受控識別系統管理員角色，請略過步驟 2-5。 系統管理員將擁有資料庫的完整存取權。

1. **[從 Azure 入口網站尋找資料處理站受控識別](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** 。 前往您資料處理站的**屬性**。 複製**受控識別應用程式識別碼** (不是**受控識別物件識別碼**)。

1. **將資料處理站受控識別轉換成二進位類型**。 使用您的 SQL/Active Directory 系統管理員帳戶，使用 SSMS 等工具連線至您受控執行個體的 **master** 資料庫。 對 **master** 資料庫執行下列 T-SQL，以二進位格式取得您的受控識別應用程式識別碼：
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. 在 Azure SQL Database 受控執行個體中**將資料處理站受控識別新增為使用者**。 對 **master** 資料庫執行下列 T-SQL：
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. **授與資料處理站受控識別所需的權限**。 對您要複製資料的資料庫執行下列 T-SQL：

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

最後，為 ADO.NET 連線管理員**設定受控識別驗證**。 有兩種選項可以執行此操作。
    
1. 在設計階段設定。 在 SSIS 設計工具中以滑鼠右鍵按一下 [ADO.NET 連線管理員]，然後按一下 [屬性]  開啟 [屬性視窗]  。 將 **ConnectUsingManagedIdentity** 屬性更新為 **True**。
    > [!NOTE]
    >  目前，當您在 SSIS 設計工具中或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 中執行 SSIS 套件時，連線管理員的 **ConnectUsingManagedIdentity** 屬性不會生效 (表示受控識別驗證無法運作)。
    
1. 在執行階段設定。 當您透過 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 或 [Azure Data Factory 執行 SSIS 套件活動](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)來執行套件時，請尋找 ADO.NET 連線管理員，並將其 **ConnectUsingManagedIdentity** 屬性更新為 **True**。
    > [!NOTE]
    >  在 Azure-SSIS 整合執行階段中，當受控識別驗證用於建立資料庫連線時，會**覆寫** ADO.NET 連線管理員上預先設定的所有其他驗證方法 (例如整合式驗證、密碼)。

> [!NOTE]
>  若要在現有套件上設定受控識別驗證，請務必至少使用[最新的 SSIS 設計工具](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)來重建您的 SSIS 專案一次，然後將 SSIS 專案重新部署至您的 Azure-SSIS 整合執行階段，以便新連線管理員的 **ConnectUsingManagedIdentity** 屬性自動新增至您 SSIS 專案中的所有 ADO.NET 連線管理員。

## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
