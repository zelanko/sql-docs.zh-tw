---
title: "刪除作業類別目錄 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 044f52ffbf373622b820014862497361316afc3f
ms.lasthandoff: 04/11/2017

---
# <a name="delete-a-job-category"></a>刪除作業類別目錄
此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、[!INCLUDE[tsql](../../includes/tsql_md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中刪除 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業類別目錄。  
  
作業類別目錄可幫助您組織作業，以便於篩選與分組。 例如，您可以將所有的資料庫備份作業整理在資料庫維護類別中。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用下列項目刪除作業類別目錄：**  
  
    [Transact-SQL](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
當您刪除使用者定義的作業類別目錄時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會提示您將已指定給該類別目錄的作業重新指定給其他作業類別目錄。 您只能刪除使用者定義的作業類別目錄。  
  
### <a name="Security"></a>Security  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-job-category"></a>若要刪除作業類別目錄  
  
1.  在 **[物件總管]**中，按一下加號展開要刪除作業類別目錄所在的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [作業]**** 資料夾，然後選取 [管理作業類別目錄]****。  
  
4.  在 [管理作業類別目錄 <伺服器名稱>]****** 對話方塊中，選取所要刪除的作業類別目錄。  
  
5.  按一下 **[刪除]**。  
  
6.  在 **[作業類別目錄]** 對話方塊中，按一下 **[是]**。  
  
7.  關閉 [管理作業類別目錄 <伺服器名稱>]****** 對話方塊。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-delete-a-job-category"></a>若要刪除作業類別目錄  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] ****。  
  
    ```  
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_delete_category (Transact-SQL)](http://msdn.microsoft.com/en-us/63ea7d0d-a567-456e-a778-bee99e21d16c)。  
  
## <a name="SMO"></a>使用 SQL Server 管理物件  
**若要刪除作業類別目錄**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 **JobCategory** 類別。  
  

