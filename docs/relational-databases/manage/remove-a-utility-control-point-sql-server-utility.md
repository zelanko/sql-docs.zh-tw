---
title: "移除公用程式控制點 (SQL Server 公用程式) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c048a416-900e-4c77-8243-e0f0d8b94068
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b38f97d5d0dacb8222faf67387c97b33d2dd5de6
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="remove-a-utility-control-point-sql-server-utility"></a>移除公用程式控制點 (SQL Server 公用程式)
  此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體移除 [!INCLUDE[tsql](../../includes/tsql-md.md)]公用程式控制點 (UCP)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目移除公用程式控制點：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 在您使用此程序從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式移除 UCP 之前，請注意下列需求。 預存程序將會在操作時執行必要條件檢查。  
  
-   在您執行此程序之前，必須從 UCP 中移除所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體。 請注意，UCP 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的受管理的執行個體。 如需詳細資訊，請參閱 [從 SQL Server 公用程式中移除 SQL Server 執行個體](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
-   此程序必須在成為 UCP 的電腦上執行。  
  
-   如果已移除 UCP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體具有非公用程式資料收集組，此程序就不會卸除 UMDW 資料庫 (sysutility_mdw)。 如果發生這種情況，您就必須先手動卸除 UMDW 資料庫 (sysutility_mdw)，然後才能再次建立 UCP。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 此程序必須由擁有系統管理員 ( **sysadmin** ) 權限的使用者執行，而這些是建立 UCP 所需的相同權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-remove-a-utility-control-point"></a>若要移除公用程式控制點  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [使用公用程式總管來管理 SQL Server 公用程式](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [疑難排解 SQL Server 公用程式](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
