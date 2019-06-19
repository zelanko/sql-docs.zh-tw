---
title: 列出作業類別目錄資訊 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 68b871d64bd0630ee7c3f478c5df49eb7e65091e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65095755"
---
# <a name="list-job-category-information"></a>列出作業類別目錄資訊
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中列出作業類別目錄資訊。  
  
-   **開始之前：**  
  
    [安全性](#Security)  
  
-   **若要使用下列項目，列出作業類別目錄資訊：**  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>安全性  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>若要列出作業類別目錄資訊  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
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
  
如需詳細資訊，請參閱 [sp_help_category (Transact-SQL)](https://msdn.microsoft.com/8cad1dcc-b43e-43bd-bea0-cb0055c84169)。  
  
## <a name="SMO"></a>使用 SQL Server 管理物件  
**若要列出作業類別目錄資訊**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **JobCategory** 類別。  
  
