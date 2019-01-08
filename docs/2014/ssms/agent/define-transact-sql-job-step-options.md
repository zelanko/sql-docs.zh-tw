---
title: 定義 Transact-SQL 作業步驟選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: b2a47057-f6fb-432b-a7b6-5d61f33a5d9c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 769e4cb9298ce2a92f7200d9e04743d6b16f842d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764480"
---
# <a name="define-transact-sql-job-step-options"></a>Define Transact-SQL Job Step Options
  此主題描述如何使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中定義 [!INCLUDE[tsql](../../includes/tsql-md.md)]  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 作業步驟的選項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目定義 Transact-SQL 作業步驟選項** ：  
  
     [Transact-SQL](#SSMS)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-define-transact-sql-job-step-options"></a>若要定義 Transact-SQL 作業步驟選項  
  
1.  在 **[物件總管]** 中，展開 **[SQL Server Agent]**，展開 **[作業]**，以滑鼠右鍵按一下要編輯的作業，然後按一下 **[屬性]**。  
  
2.  按一下 **[步驟]** 頁面，再按一下作業步驟，然後按一下 **[編輯]**。  
  
3.  在 **[作業步驟屬性]** 對話方塊中，確認作業類型是 **Transact-SQL script (TSQL)**，然後選取 **[進階]** 頁面。  
  
4.  從 **[成功時的動作]** 清單中，指定當作業成功時要採取的動作。  
  
5.  在 **[重試次數]** 方塊中輸入 0 到 9999 之間的數字，以指定重試次數。  
  
6.  在 **[重試間隔]** 方塊中輸入 0 到 9999 的分鐘數，以指定重試間隔。  
  
7.  從 **[失敗時的動作]** 清單中，指定當作業失敗時要採取的動作。  
  
8.  如果作業是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，您可以從下列選項中選擇：  
  
    -   輸入 **[輸出檔案]** 的名稱。 根據預設，每次執行作業步驟時都會覆寫此檔案。 如果您不想要覆寫輸出檔，請選取 **[將輸出附加至現有檔案]**。 此選項僅適用於 **系統管理員 (sysadmin)** 固定伺服器角色的成員。 請注意， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 不允許使用者檢視檔案系統上的任意檔案，所以您不能使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來檢視已寫入檔案系統的作業步驟記錄檔。  
  
    -   若要將作業步驟記錄至資料庫資料表，請選取 **[記錄至資料表]** 。 根據預設，每次執行作業步驟時都會覆寫此資料表內容。 如果您不想要覆寫資料表內容，請選取 **[將輸出附加至資料表的現有項目]**。 作業步驟執行之後，您可以按一下 **[檢視]** 以檢視這個資料表的內容。  
  
    -   如果您希望步驟的記錄中包含輸出，請選取 **[包含步驟輸出於記錄中]** 。 只有無錯誤時，才會顯示輸出。 另外，輸出可能被截斷。  
  
9. 如果您是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，而您想以不同的 SQL 登入執行這個作業步驟，請從 **[指定執行時的身分]** 清單中選取 SQL 登入。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要定義 Transact-SQL 作業步驟選項**  
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `JobStep` 類別。  
  
  
