---
title: 在 SQL Server Agent 中執行 Windows PowerShell 步驟 | Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a72a0b791c545e620e7d11600768845d2dabe3d7
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730551"
---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>在 SQL Server Agent 中執行 Windows PowerShell 步驟

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

使用 SQL Server Agent 在排定的時間執行 SQL Server PowerShell 指令碼。  
  
**若要從 SQL Server Agent 執行 PowerShell，請使用：** [PowerShell 作業步驟](#PShellJob)、[命令提示字元作業步驟](#CmdExecJob)  
  
> [!IMPORTANT]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。  
> 舊版 **SqlServer** 模組隨附於  SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
> 若要安裝 **SqlServer** 模組，請參閱[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)。


[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業步驟有幾種類型。 每一種類型都與實作特定環境的子系統相關，例如複寫代理程式或命令提示字元環境。 您可以編寫 Windows PowerShell 指令碼，然後使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 在排程時間執行的作業內包含這些指令碼，或是用來回應 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 事件。 Windows PowerShell 指令碼可透過使用命令提示字元作業步驟或 PowerShell 作業步驟加以執行。  

- 使用 PowerShell 作業步驟讓 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理程式子系統執行 **sqlps** 公用程式，此公用程式會啟動 PowerShell 並匯入 **sqlps** 模組。

- 使用命令提示字元作業步驟執行 PowerShell.exe，並指定匯入 **sqlps** 模組的指令碼。

### <a name="LimitationsRestrictions"></a> 請注意記憶體耗用量

搭配 **sqlps** 模組執行 PowerShell 的每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業步驟，都會啟動大約耗用 **20 MB** 記憶體的處理序。 執行大量的並行 Windows PowerShell 作業步驟可能會對效能造成負面影響。  

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="PShellJob"></a> 建立 PowerShell 作業步驟  
 **建立 PowerShell 作業步驟**  
  
1.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]  。 如需建立作業的詳細資訊，請參閱＜ [建立作業](../ssms/agent/create-jobs.md)＞。  
  
2.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]** 。  
  
3.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
4.  在 **[類型]** 清單中，按一下 **[PowerShell]** 。  
  
5.  在 **[執行身分]** 清單中，選取具有作業將會使用之認證的 Proxy 帳戶。  
  
6.  在 **[命令]** 方塊中，輸入將為作業步驟執行的 PowerShell 指令碼語法。 或者，請按一下 **[開啟舊檔]** ，然後選取包含指令碼語法的檔案。  
  
7.  按一下 **[進階]** 頁面，設定下列作業步驟選項：作業步驟成功或失敗時要採取什麼動作、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 應該嘗試執行作業步驟多少次，以及應該多久重試一次。  
  
##  <a name="CmdExecJob"></a> 建立命令提示字元作業步驟  
 **建立 CmdExec 作業步驟**  
  
1.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]  。 如需建立作業的詳細資訊，請參閱＜ [建立作業](../ssms/agent/create-jobs.md)＞。  
  
2.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]** 。  
  
3.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
4.  在 [類型]  清單中，選擇 [作業系統 (CmdExec)]  。  
  
5.  在 **[執行身分]** 清單中，選取具有作業將會使用之認證的 Proxy 帳戶。 根據預設，CmdExec 作業步驟會以 SQL Server Agent 服務帳戶的身分執行。  
  
6.  在 **[成功命令的處理序結束碼]** 方塊中，輸入介於 0 到 999999 之間的值。  
  
7.  在 **[命令]** 方塊中，輸入內含指定執行 PowerShell 指令碼之參數的 powershell.exe。  
  
8.  按一下 **[進階]** 頁面設定作業步驟選項，例如：作業步驟成功或失敗時要採取什麼動作、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 應該嘗試執行作業步驟多少次，以及可供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 寫入作業步驟輸出的檔案。 只有 **sysadmin** 固定伺服器角色的成員，可以將作業步驟輸出寫入作業系統檔案。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
