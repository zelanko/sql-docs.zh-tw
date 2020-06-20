---
title: 設定警示呼叫器號碼的格式 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3754afbc5d8f0f67dac61e785a4626c8ced4c2e9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995295"
---
# <a name="format-pager-addresses-for-alerts"></a>設定警示的呼叫器位址格式
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或，在中格式化 Agent 警示的呼機位址 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目，格式化呼叫器號碼：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 依預設， **系統管理員 (sysadmin)** 固定伺服器角色的成員可以檢視警示的相關資訊。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>若要格式化呼叫器號碼  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含要傳送至呼叫器的警示。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]****，然後選取 [屬性]****。  
  
3.  在 **[選取頁面]** 底下，選取 **[警示系統]**。  
  
4.  在 [呼叫器電子郵件位址格式]**** 欄位的 [收件者]**** 和 [副本]**** 方塊中，輸入呼叫器號碼的前置詞和後置詞。 當傳送通知時，就會插入操作員的實際呼叫器號碼。  
  
5.  在 **[主旨]** 方塊中，輸入主旨行前置詞或後置詞。  
  
6.  選取 [將電子郵件的內文包含在通知訊息中]**** 核取方塊，表示會在呼叫器訊息中加入完整的電子郵件訊息 (而不是僅有主旨行)。  
  
7.  完成時按一下 **[確定]**。  
  
  
