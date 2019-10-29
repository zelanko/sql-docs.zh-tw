---
title: 在 SQL Server 中進行驗證
description: 描述 SQL Server 中的登入和驗證，並提供其他資源的連結。
ms.date: 09/26/2019
dev_langs:
- csharp
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: eb528eb1045788469b0eb31491fd654997831468
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452317"
---
# <a name="authentication-in-sql-server"></a>在 SQL Server 中進行驗證

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 支援兩種驗證模式：Windows 驗證模式和混合模式。  
  
- Windows 驗證是預設設定，也經常稱為整合式安全性，原因為這個 SQL Server 安全性模型會與 Windows 緊密整合。 特定的 Windows 使用者和群組帳戶受信任，可登入 SQL Server。 已通過驗證的 Windows 使用者不需要出示額外的認證。  
  
- 混合模式支援 Windows 和 SQL Server 提供的驗證。 使用者名稱和密碼組會在 SQL Server 內進行維護。  
  
> [!IMPORTANT]
> 我們建議盡可能使用 Windows 驗證。 Windows 驗證會使用一系列的加密訊息在 SQL Server 中驗證使用者。 使用 SQL Server 登入時，SQL Server 登入名稱及加密密碼會透過網路傳遞，因而降低其安全性。  
  
使用 Windows 驗證的好處是因為使用者已登入 Windows，所以不必再另行登入 SQL Server。 下列 `SqlConnection.ConnectionString` 可指定 Windows 驗證，且不需要使用者提供使用者名稱或密碼。  
  
```csharp
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
> 登入與資料庫使用者不同。 您必須在個別的作業中，將登入或 Windows 群組對應至資料庫使用者或角色。 接著，您可以將許可權授與使用者或角色，以存取資料庫物件。  
  
## <a name="authentication-scenarios"></a>驗證案例  
在下列情況下，Windows 驗證通常是最佳選擇：  
  
- 有一個網域控制站。  
  
- 應用程式和資料庫位於相同的電腦上。  
  
- 您使用的是 SQL Server Express 或 LocalDB 執行個體。  
  
在下列情況下，通常會使用 SQL Server 登入：  
  
- 如果您有工作組。  
  
- 使用者從不同、不受信任的網域進行連接。  
  
- 網際網路應用程式，例如 ASP.NET。  
  
> [!NOTE]
> 指定 Windows 驗證並不會停用 SQL Server 登入。 請使用 ALTER LOGIN DISABLE Transact-SQL 陳述式來停用具有高權限的 SQL Server 登入。  
  
## <a name="login-types"></a>登入類型  
SQL Server 支援三種登入類型：  
  
- 本機 Windows 使用者帳戶或受信任的網域帳戶。 SQL Server 會仰賴 Windows 來驗證 Windows 使用者帳戶。  
  
- Windows 群組。 授與 Windows 群組的存取權，可授與屬於群組成員之所有 Windows 使用者登入的存取權。  
  
- SQL Server 登入。 SQL Server 會使用內部驗證方法確認登入作業，將使用者名稱和密碼雜湊儲存在 master 資料庫。  
  
> [!NOTE]
> SQL Server 提供從憑證建立的登入或非對稱金鑰，這些項目只能用於程式碼簽署。 它們不能用來連線至 SQL Server。  
  
## <a name="mixed-mode-authentication"></a>混合模式驗證  
如果您必須使用混合模式驗證，則必須建立儲存在 SQL Server 中的 SQL Server 登入。 然後在執行階段時還需要提供 SQL Server 使用者名稱和密碼。  
  
> [!IMPORTANT]
> SQL Server 會使用名為 `sa` 的 SQL Server 登入進行安裝（「系統管理員」的縮寫）。 將強式密碼指派給 `sa` 登入，而不要在您的應用程式中使用 `sa` 登入。 `sa` 登入對應到 `sysadmin` 固定伺服器角色，這在整個伺服器上具有無法撤銷的系統管理認證。 如果攻擊者取得系統管理員的存取權，就不會有潛在損害的限制。 Windows `BUILTIN\Administrators` 群組 (本機系統管理員群組) 的所有成員，都會預設為 `sysadmin` 角色的成員，但可以從該角色移除。  
  
> [!IMPORTANT]
> 串連來自使用者輸入的連接字串，可能會讓您容易遭受連接字串插入式攻擊。 使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>，在執行時間建立語法有效的連接字串。 
  
## <a name="external-resources"></a>外部資源  
如需詳細資訊，請參閱下列資源。  
  
|資源|Description|  
|--------------|-----------------|  
|[主體](../../../relational-databases/security/authentication-access/principals-database-engine.md)|說明 SQL Server 中的登入及其他安全性主體。|  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的應用程式安全性案例](application-security-scenarios-sql-server.md)
