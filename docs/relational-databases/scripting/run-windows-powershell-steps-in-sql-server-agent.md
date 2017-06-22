---
title: "在 SQL Server Agent 中執行 Windows PowerShell 步驟 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae35fb3deecc8b77940ab76d1b0f016f00f39e27
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>在 SQL Server Agent 中執行 Windows PowerShell 步驟
  使用 SQL Server Agent 在排定的時間執行 SQL Server PowerShell 指令碼。  
  
1.  **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions)  
  
2.  **To run PowerShell from SQL Server Agent, using:**  [PowerShell Job Step](#PShellJob), [Command Prompt Job Step](#CmdExecJob)  
  
## <a name="before-you-begin"></a>開始之前  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟有幾種類型。 每一種類型都與實作特定環境的子系統相關，例如複寫代理程式或命令提示字元環境。 您可以編寫 Windows PowerShell 指令碼，然後使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在排程時間執行的作業內包含這些指令碼，或是用來回應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 Windows PowerShell 指令碼可透過使用命令提示字元作業步驟或 PowerShell 作業步驟加以執行。  
  
1.  使用 PowerShell 作業步驟讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式子系統執行 **sqlps** 公用程式，此公用程式會啟動 PowerShell 並匯入 **sqlps** 模組。  
  
2.  使用命令提示字元作業步驟執行 PowerShell.exe，並指定匯入 **sqlps** 模組的指令碼。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
  
> [!CAUTION]  
>  搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 模組執行 PowerShell 的每項 **sqlps** Agent 作業步驟，都會啟動大約耗用 20 MB 記憶體的處理序。 執行大量的並行 Windows PowerShell 作業步驟可能會對效能造成負面影響。  
  
##  <a name="PShellJob"></a> 建立 PowerShell 作業步驟  
 **建立 PowerShell 作業步驟**  
  
1.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]。 如需建立作業的詳細資訊，請參閱＜ [建立作業](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b)＞。  
  
2.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]**。  
  
3.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
4.  在 **[類型]** 清單中，按一下 **[PowerShell]**。  
  
5.  在 **[執行身分]** 清單中，選取具有作業將會使用之認證的 Proxy 帳戶。  
  
6.  在 **[命令]** 方塊中，輸入將為作業步驟執行的 PowerShell 指令碼語法。 或者，請按一下 **[開啟舊檔]** ，然後選取包含指令碼語法的檔案。  
  
7.  按一下 **[進階]** 頁面，設定下列作業步驟選項：作業步驟成功或失敗時要採取什麼動作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 應該嘗試執行作業步驟多少次，以及應該多久重試一次。  
  
##  <a name="CmdExecJob"></a> 建立命令提示字元作業步驟  
 **建立 CmdExec 作業步驟**  
  
1.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]。 如需建立作業的詳細資訊，請參閱＜ [建立作業](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b)＞。  
  
2.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]**。  
  
3.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
4.  在 [類型] 清單中，選擇 [作業系統 (CmdExec)]。  
  
5.  在 **[執行身分]** 清單中，選取具有作業將會使用之認證的 Proxy 帳戶。 根據預設，CmdExec 作業步驟會以 SQL Server Agent 服務帳戶的身分執行。  
  
6.  在 **[成功命令的處理序結束碼]** 方塊中，輸入介於 0 到 999999 之間的值。  
  
7.  在 **[命令]** 方塊中，輸入內含指定執行 PowerShell 指令碼之參數的 powershell.exe。  
  
8.  按一下 **[進階]** 頁面設定作業步驟選項，例如：作業步驟成功或失敗時要採取什麼動作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 應該嘗試執行作業步驟多少次，以及可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 寫入作業步驟輸出的檔案。 只有 **sysadmin** 固定伺服器角色的成員，可以將作業步驟輸出寫入作業系統檔案。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
