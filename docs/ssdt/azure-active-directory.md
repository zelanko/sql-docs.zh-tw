---
title: SQL Server Data Tools (SSDT) 中的 Azure Active Directory 支援 | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1e8f19c1dcc629ec6e97aa02cd23be1c101ad596
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 中的 Azure Active Directory 支援

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md.md](../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

SQL Server Data Tools (SSDT) 提供數個 [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) 驗證方法。

![SSDT 連線對話方塊](media/azure-active-directory/interactive.png)

## <a name="active-directory-password-authentication"></a>Active Directory 密碼驗證

Active Directory 密碼驗證是使用 Azure Active Directory (Azure AD) 中的身分識別連線至 Azure SQL Database 的機制。  如果您用來登入 Windows 的認證來自未與 Azure 同盟的網域，或是使用 Azure AD 根據初始或用戶端網域來使用 Azure AD 驗證時，請使用此方法連線。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。  

## <a name="active-directory-integrated-authentication"></a>Active Directory 整合式驗證

Active Directory 整合式驗證是使用 Azure Active Directory (Azure AD) 中的身分識別連線至 Azure SQL Database 的機制。 如果您使用來自同盟網域的 Azure Active Directory 認證登入 Windows，請使用此方法連線。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。

## <a name="active-directory-interactive-authentication-preview"></a>Active Directory 互動式驗證 (預覽)

SSDT 提供連線到 Azure SQL 資料庫的新驗證方法 - **Active Directory 互動式驗證**。


> [!NOTE]
> 在 [Visual Studio 2017 preview](https://www.visualstudio.com/vs/preview/) 中與 SSDT 連線時，便可以使用 Active Directory 互動式驗證，且執行 SSDT 的電腦上必須已經安裝 [.NET 4.7.2 預覽 (KB4038188)](https://go.microsoft.com/fwlink/?linkid=867317)。 如果未安裝 .NET 4.7.2 預覽 (KB4038188)，將無法使用 Active Directory 互動式驗證選項。


Active Directory 互動式驗證支援互動式驗證，允許使用 Azure Active Directory (AD) 多重要素驗證 (MFA) 向 Azure SQL Database 驗證。 這個方法支援原生和同盟的 Azure AD 使用者和來自其他帳戶的來賓使用者 (包括 B2B 使用者、Microsoft 和非 Microsoft 帳戶，例如 @outlook.com、@hotmail.com、@live.com，及 @gmail.com)。 如果指定此方法，就必須指定 [使用者名稱]，而 [密碼] 欄位會被停用。 

向「Active Directory 互動式驗證」驗證時，會開啟要求使用者手動輸入密碼的驗證視窗。

![登入對話方塊](media/azure-active-directory/sign-in.png)

在驗證程序期間，MFA 強制執行是由 Azure AD 透過此額外的 MFA 快顯示窗來提供。

> [!NOTE]
> 因為「Active Directory 互動式驗證」需要使用者手動 (互動地) 輸入密碼，因此不建議將它用於自動化工作流程。


## <a name="known-issues-and-limitations"></a>已知問題和限制

- 當連線到 Azure SQL 資料庫時，才支援「Active Directory 互動式驗證」。 它不支援 SQL Server (內部部署或在 VM 上)，或 Azure SQL 資料倉儲。
- 在 [伺服器總管] 中的連線對話方塊中不支援「Active Directory 互動式驗證」，您必須搭配使用 SSDT 和「SQL Server 物件總管」來連線。
- 與目前登入 Visual Studio 帳戶的單一登入整合不支援 SSDT。
- 在 Visual Studio 安裝期間安裝到 Extensions 目錄的 SQLPackage.exe，並不是要從該位置使用。 若要以 AAD 使用 SQLpackage.exe，請前往 https://www.microsoft.com/en-us/download/details.aspx?id=55088 
- 「SSDT 資料比較」不支援包含新驗證方法的 AAD 驗證。  





## <a name="see-also"></a>另請參閱  
[多重要素驗證](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[搭配使用 Azure Active Directory 驗證和 SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[Visual Studio 中的 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 團隊部落格](http://blogs.msdn.com/b/ssdt/)  
[DACFx API 參考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
