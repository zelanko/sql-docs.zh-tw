---
title: 列出作業類別目錄資訊 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 231143d7b7fb90f8da6a614d047b98f9da22dbb0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022112"
---
# <a name="list-job-category-information"></a>列出作業類別目錄資訊
  如何列出作業類別目錄資訊中的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]或 SQL Server 管理物件。  

  
##  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  

  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>若要列出作業類別目錄資訊  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_help_category &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql)。  
  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要列出作業類別目錄資訊**  
  
 使用`JobCategory`使用您選擇，例如 Visual Basic、 Visual C# 或 PowerShell 的程式語言的類別... 如需詳細資訊，請參閱[SQL Server 管理物件&#40;SMO&#41;程式設計指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
  
  
  
