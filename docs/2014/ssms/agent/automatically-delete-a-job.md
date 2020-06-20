---
title: 自動刪除作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- dropping jobs
- SQL Server Agent jobs, removing
- automatic job removal
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 92dbb6da-5919-4bde-9354-d454e9ea3da0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42538ac6566b70105fd183da1cadd00f7fd0c13b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011785"
---
# <a name="automatically-delete-a-job"></a>自動刪除作業
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或 SQL Server 管理物件，在中設定 Agent 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 作業成功、失敗或完成時自動予以刪除 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
 作業回應可確保資料庫管理員知道作業已完成，以及作業的執行頻率。 典型的作業回應包括：  
  
-   使用電子郵件、電子呼叫或 **net send** 訊息通知操作員。  
  
     如果操作員必須執行後續動作，請使用其中一個作業回應。 例如，如果備份作業成功完成，必須告知操作員以取下備份磁帶，並將其存放在安全的地方。  
  
-   將事件訊息寫入至 Windows 應用程式記錄。  
  
     這個回應只用於失敗的作業。  
  
-   自動刪除作業。  
  
     如果確定您將不再需要重新執行這個作業，請使用這個作業回應。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目指定作業回應：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-automatically-delete-a-job"></a>若要自動刪除作業  
  
1.  在 [物件總管]**** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，展開 **[作業]**，以滑鼠右鍵按一下要編輯的作業，然後按一下 **[屬性]**。  
  
3.  選取 **[通知]** 頁面。  
  
4.  選取 **[自動刪除作業]**，然後選擇下列其中一項：  
  
    -   按一下 **[當作業成功時]** ，以便在作業順利完成時刪除作業狀態。  
  
    -   按一下 **[當作業失敗時]** ，以便在作業未順利完成時刪除作業。  
  
    -   按一下 **[作業完成時]** ，不管完成狀態為何都刪除作業。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
 **若要自動刪除作業**  
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `DeleteLevel` 類別的 `Job` 屬性。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
