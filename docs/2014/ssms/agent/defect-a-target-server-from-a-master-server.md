---
title: 使目標伺服器脫離主要伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2b17703fa87f5c0d3e7146a1660ac1ca7c7c1d81
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008931"
---
# <a name="defect-a-target-server-from-a-master-server"></a>使目標伺服器脫離主要伺服器
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理物件 (SMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中從主伺服器脫離目標伺服器。 請從目標伺服器執行這個程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法脫離目標伺服器：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要執行這個預存程序，使用者必須是 `sysadmin` (系統管理員) 固定伺服器角色的成員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>若要使目標伺服器脫離主伺服器  
  
1.  在 **[物件總管]** 中，展開設定為目標伺服器的伺服器。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]**，指向 **[多伺服器管理]**，然後按一下 **[脫離]**。  
  
3.  按一下 **[是]** 以確定您要從主要伺服器脫離這台目標伺服器。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>若要使目標伺服器脫離主伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
```sql
sp_msx_defect ;  
```  
  
 如需詳細資訊，請參閱[sp_msx_defect &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-defect-transact-sql)。  
  
##  <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>使用 SQL Server 管理物件（SMO）  
 請使用 `MsxDefect Method`。  
  
## <a name="see-also"></a>另請參閱  
 [建立多伺服器環境](create-a-multiserver-environment.md)   
 [跨企業進行自動化管理](automated-administration-across-an-enterprise.md)   
 [從主要伺服器脫離多個目標伺服器](defect-multiple-target-servers-from-a-master-server.md)  
