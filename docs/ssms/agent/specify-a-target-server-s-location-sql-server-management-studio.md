---
title: "指定目標伺服器位置 | Microsoft Docs"
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
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e287e48b3185904eb2fb5b24920aa3dca433fcff
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="specify-a-target-server39s-location-sql-server-management-studio"></a>指定目標伺服器的位置 (SQL Server Management Studio)
此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql_md.md)]中於多伺服器管理組態指定目標伺服器的位置。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用下列項目指定目標伺服器的位置：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
執行此動作會編輯登錄。 您最好不要手動編輯登錄，因為不當或不正確的變更會使系統發生嚴重的組態問題。 因此，只有資深使用者才應該利用登錄編輯器程式來編輯登錄。 如需詳細資訊，請參閱 Microsoft Windows 文件集。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-specify-a-target-servers-location"></a>若要指定目標伺服器的位置  
  
1.  在 **[物件總管]**中，按一下加號，展開要指定目標伺服器位置的主要伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]、指向 [多伺服器管理]，然後選取 [管理目標伺服器]。  
  
3.  以滑鼠右鍵按一下目標伺服器，然後選取 [屬性]。  
  
4.  在 **[位置]** 方塊中輸入伺服器的位置，再按一下 **[確定]**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-specify-a-target-servers-location"></a>若要指定目標伺服器的位置  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE msdb ;  
    GO  
    -- enlists the current server into the AdventureWorks1 master server.   
    -- The location for the current server is Building 21, Room 309, Rack 5  
    EXEC dbo.sp_msx_enlist N'AdventureWorks2012',   
        N'Building 21, Room 309, Rack 5' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)。  
  

