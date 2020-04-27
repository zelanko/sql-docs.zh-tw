---
title: 設定作業執行關機 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca9343fe8a6f9e89ba9f26dbbbb12dd7362aff91
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63033597"
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>設定作業執行關機 (SQL Server Management Studio)
  本主題描述如何使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在中設定 agent 等待執行中作業完成的時間，然後 agent 本身才會完成。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目設定 SQL Server Agent 作業的關機時間：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 根據預設，**系統管理員**固定伺服器角色成員可以設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 等待執行中作業完成的等候時間，之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 便會自行結束。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>若要設定作業執行關機  
  
1.  在 **[物件總管]** 中，按一下加號，展開要設定作業執行關機間隔的伺服器。  
  
2.  以滑鼠右鍵按一下**SQL Server Agent** ，然後選取 [**屬性**]。  
  
3.  在 **[選取頁面]** 底下，選取 **[作業的系統]**。  
  
4.  設定 [關機逾時間隔]**** \(以秒為單位)，以增加或減少關機的逾時間隔。 這決定了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 自行結束前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會等待執行中作業完成的時間。  
  
  
