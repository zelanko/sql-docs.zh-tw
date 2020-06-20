---
title: 列出作業類別目錄資訊 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 924e2b064980b2ea7068230610414262995da1a6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008715"
---
# <a name="list-job-category-information"></a>列出作業類別目錄資訊
  如何 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用或 SQL Server 管理物件，在中列出作業類別目錄資訊 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  

  
##  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  

  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>若要列出作業類別目錄資訊  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_help_category &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql)。  
  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
 **若要列出作業類別目錄資訊**  
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `JobCategory` 類別。 如需詳細資訊，請參閱[SQL Server 管理物件 &#40;SMO&#41; 程式設計手冊](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
