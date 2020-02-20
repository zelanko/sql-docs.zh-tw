---
title: SSDT 中的 Azure Active Directory
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: jroth
reviewer: ''
ms.custom: seo-lt-2019
ms.date: 10/28/2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ed7bc77b48881351a144ed5d217454518abafcc2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75245580"
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 中的 Azure Active Directory 支援

[!INCLUDE[appliesto-xx-asdb-asdb-xxx-md.md](../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

SQL Server Data Tools (SSDT) 提供數個 [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) 驗證方法。

在 Visual Studio 中，開啟 [SQL Server 物件總管]  (位於 [檢視]  功能表)，然後選取 [新增 SQL Server]  ：

![SSDT 連線對話方塊](media/azure-active-directory/interactive.png)

#### <a name="which-azure-sql-products"></a>哪些 Azure SQL 產品？

本文討論 [Azure 雲端](https://azure.microsoft.com/)中適用於下列「Azure SQL 產品」  清單的 Azure AD：

- Azure SQL Database
- Azure SQL 資料倉儲

## <a name="active-directory-password-authentication"></a>Active Directory 密碼驗證

「Active Directory 密碼驗證」  是連線到稍早所列 Azure SQL 產品的機制。 該機制使用 Azure Active Directory (Azure AD) 中的身分識別。 在下列情況下，請使用此方法連線：

- 您從未與 Azure 同盟的網域中使用認證來登入 Windows，或
- 您針對 Azure AD 使用 Azure AD 驗證，而它是以初始或用戶端網域為依據。

如需詳細資訊，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。  

## <a name="active-directory-integrated-authentication"></a>Active Directory 整合式驗證

「Active Directory 整合式驗證」  是使用 Azure Active Directory (Azure AD) 中的身分識別連線到所列 Azure SQL 產品的機制。 如果您使用來自同盟網域的 Azure Active Directory 認證登入 Windows，請使用此方法連線。 如需詳細資訊，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。

## <a name="active-directory-interactive-authentication"></a>Active Directory 互動式驗證

「Active Directory 互動式驗證」  適用於使用 SSDT 連線到所列 Azure SQL 產品的情況，但僅限於 [.NET Framework 4.7.2](https://docs.microsoft.com/dotnet/api/?view=netframework-4.7.2) 或更新版本。

- [下載並安裝 .NET Framework 的任何版本](https://www.microsoft.com/net/download/all)。
- [Visual Studio 2017 15.6 版](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes)或更新版本。

#### <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)

Active Directory 互動式驗證支援互動式驗證，可讓您使用 Azure Active Directory (AD) Multi-Factor Authentication (MFA) 向所列的 Azure SQL 產品驗證。 此方法支援原生和同盟的 Azure AD 使用者，以及來自其他帳戶的來賓使用者。 其他類型的帳戶還包括：

- 企業對企業 (Azure AD B2B) 使用者。
- Microsoft 帳戶，例如@outlook.com、@hotmail.com、@live.com。
- 非 Microsoft 帳戶，例如 @gmail.com。

如果指定 MFA 方法，就必須指定 [使用者名稱]  ，而 [密碼]  欄位則會停用。 

#### <a name="password-entry"></a>密碼項目

向「Active Directory 互動式驗證」  驗證時，會開啟要求使用者手動輸入密碼的驗證視窗。

![登入對話方塊](media/azure-active-directory/sign-in.png)

MFA 強制執行是由 Azure AD 透過此額外的 MFA 快顯視窗來提供。

> [!NOTE]
> 使用「Active Directory 互動式驗證」  會封鎖自動化工作流程。 必須有可手動輸入密碼來與驗證程序互動的人員。

## <a name="known-issues-and-limitations"></a>已知問題和限制

- 只有在連線到本文開頭所列的 Azure SQL 產品時，才支援「Active Directory 互動式驗證」  。 SQL Server (內部部署或 VM 上) 不提供支援。
- [伺服器總管]  的連線對話方塊中不支援「Active Directory 互動式驗證」  。 您必須搭配使用 SSDT 和 [SQL Server 物件總管]  來連線。
- 與目前登入 Visual Studio 帳戶的單一登入整合不支援 SSDT。
- 在 Visual Studio 安裝期間安裝到 Extensions 目錄的 SQLPackage.exe，並不是要從該位置使用。 若要以 Azure AD 使用 SQLPackage.exe，請前往 [https://www.microsoft.com/download/details.aspx?id=55088](https://www.microsoft.com/download/details.aspx?id=55088) 
- Azure AD 驗證不支援 SSDT 資料比較。  


## <a name="see-also"></a>另請參閱  

[多重要素驗證](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[搭配使用 Azure Active Directory 驗證和 SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[SSDT MSDN 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 團隊部落格](https://blogs.msdn.com/b/ssdt/)  
[DACFx API 參考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
