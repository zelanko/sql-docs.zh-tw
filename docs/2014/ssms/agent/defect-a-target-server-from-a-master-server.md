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
manager: craigg
ms.openlocfilehash: 3f51e8f62a6be442c123c5a1309293e204caf08f
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783223"
---
# <a name="defect-a-target-server-from-a-master-server"></a>Defect a Target Server from a Master Server
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQL Server 管理物件 (SMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中從主伺服器脫離目標伺服器。 請從目標伺服器執行這個程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法脫離目標伺服器：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> Permissions  
 若要執行這個預存程序，使用者必須是 `sysadmin` (系統管理員) 固定伺服器角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>若要使目標伺服器脫離主伺服器  
  
1.  在 **[物件總管]** 中，展開設定為目標伺服器的伺服器。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]** ，指向 **[多伺服器管理]** ，然後按一下 **[脫離]** 。  
  
3.  按一下 **[是]** 以確定您要從主要伺服器脫離這台目標伺服器。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>若要使目標伺服器脫離主伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行]。  
  
```sql
sp_msx_defect ;  
```  
  
 如需詳細資訊，請參閱[sp_msx_defect &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-defect-transact-sql)。  
  
##  <a name="PowerShellProcedure"></a>使用 SQL Server 管理物件（SMO）  
 請使用 `MsxDefect Method`。  
  
## <a name="see-also"></a>另請參閱  
 [建立多伺服器環境](create-a-multiserver-environment.md)   
 [將整個企業的管理自動化](automated-administration-across-an-enterprise.md)   
 [使多個目標伺服器脫離主要伺服器](defect-multiple-target-servers-from-a-master-server.md)  
