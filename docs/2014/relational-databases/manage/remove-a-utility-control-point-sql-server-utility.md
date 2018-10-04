---
title: 移除公用程式控制點 (SQL Server 公用程式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c048a416-900e-4c77-8243-e0f0d8b94068
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 719e50f8423a320abfb2476402cc437e1f2520a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229568"
---
# <a name="remove-a-utility-control-point-sql-server-utility"></a>移除公用程式控制點 (SQL Server 公用程式)
  此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體移除 [!INCLUDE[tsql](../../includes/tsql-md.md)]公用程式控制點 (UCP)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目移除公用程式控制點：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 在您使用此程序從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式移除 UCP 之前，請注意下列需求。 預存程序將會在操作時執行必要條件檢查。  
  
-   在您執行此程序之前，必須從 UCP 中移除所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體。 請注意，UCP 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的受管理的執行個體。 如需詳細資訊，請參閱 [從 SQL Server 公用程式中移除 SQL Server 執行個體](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
-   此程序必須在成為 UCP 的電腦上執行。  
  
-   如果已移除 UCP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體具有非公用程式資料收集組，此程序就不會卸除 UMDW 資料庫 (sysutility_mdw)。 如果發生這種情況，您就必須先手動卸除 UMDW 資料庫 (sysutility_mdw)，然後才能再次建立 UCP。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 此程序必須由具有的使用者執行`sysadmin`權限; 建立 UCP 所需的相同權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-remove-a-utility-control-point"></a>若要移除公用程式控制點  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)   
 [使用公用程式總管來管理 SQL Server 公用程式](use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [疑難排解 SQL Server 公用程式](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
