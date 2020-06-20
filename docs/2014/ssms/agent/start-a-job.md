---
title: 啟動作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4d5af895df518a915dacd953331b9139471933aa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058665"
---
# <a name="start-a-job"></a>啟動作業
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理物件，在中開始執行 Agent 作業 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 作業是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行的一系列指定動作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業可以在本機伺服器或多個遠端伺服器上執行。  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目啟動作業：**  
  
     [Transact-SQL](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
### <a name="to-start-a-job"></a>若要啟動作業  
  
1.  在 [物件總管]**** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]** ，再展開 **[作業]**。 請依照您所需要的作業啟動方式，執行下列其中一項作：  
  
    -   若要對單一伺服器或目標伺服器執行作業，或要在主要伺服器上執行本機伺服器作業，請在要啟動的作業上按一下滑鼠右鍵，然後按一下 [啟動作業]****。  
  
    -   若要啟動多項作業，請在 [作業活動監視器]****，然後按一下 [檢視作業活動]****。 您可以在作業活動監視器中選取多項作業，然後在選取範圍上按一下滑鼠右鍵，再按一下 [啟動作業]****。  
  
    -   若要對主要伺服器執行作業，並希望所有目標伺服器同時執行該作業，請在要啟動的作業上按一下滑鼠右鍵，然後按一下 [啟動作業]****，再按一下 [在所有目標伺服器上啟動]****。  
  
    -   若要對主要伺服器執行作業，並要指定執行該作業的目標伺服器，請在要啟動的作業上按一下滑鼠右鍵，然後按一下 [啟動作業]****，再按一下 [在特定目標伺服器上啟動]****。 在 **[公佈下載指示]** 對話方塊中選取 **[下列目標伺服器]** 核取方塊，然後選取應該執行此作業的每個目標伺服器。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
### <a name="to-start-a-job"></a>若要啟動作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  

### <a name="to-start-a-job"></a>若要啟動作業
  
 使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 `Start` 類別的 `Job` 方法。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
