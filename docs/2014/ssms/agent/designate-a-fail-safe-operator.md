---
title: 指定保全操作員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73eb11034d185deb9c004d138230fff8fbf27bb6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995285"
---
# <a name="designate-a-fail-safe-operator"></a>指定保全操作員
  如果在無法聯繫到指定的操作員時，就會由保全操作員這位使用者接收警示。 本主題描述如何使用，在中設定要接收 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示通知的失敗安全操作員 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目指定保全操作員：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   在未來版本的中，將會從 Agent 移除 [呼機] 和 [ **net send** ] 選項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
-   請注意，必須設定 SQL Server Agent 使用 Database Mail，才能將電子郵件及呼叫器通知傳送給操作員。 如需詳細資訊，請參閱＜ [指派警示給操作員](assign-alerts-to-an-operator.md)＞。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員才能指定保全操作員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>若要指定保全操作員  
  
1.  在物件總管**** 中，按一下加號，展開包含要指定為保全操作員之 SQL Server Agent 操作員的伺服器。  
  
2.  以滑鼠右鍵按一下**SQL Server Agent** ，然後選取 [**屬性**]。  

3.  在 [ **SQL Server Agent 屬性-**_server_name_ ] 對話方塊的 [**選取頁面**] 底下，選取 [**警示系統**]。  
 
4.  在 [保全操作員]**** 下方，選取 [啟用保全操作員]****。  
  
5.  在 [操作員]**** 清單中，選取您想要設為保全操作員的操作員。  
  
6.  選取下列任何一個或所有核取方塊，指定通知操作員的方法：[電子郵件]****、[呼叫器]**** 或 [Net send]****。  
  
7.  完成時按一下 **[確定]**。  
  
  
