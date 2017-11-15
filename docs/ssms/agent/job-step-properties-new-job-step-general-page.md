---
title: "作業步驟屬性 - 新增作業步驟 (一般頁面) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.job.stepgeneral.f1
ms.assetid: 8d1885ba-4386-4528-8f2b-68c16852720c
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6821abbd0c69929350a95c004033e730e6ff769
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="job-step-properties---new-job-step-general-page"></a>作業步驟屬性 - 新增作業步驟 (一般頁面)
使用此頁面來檢視和變更 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理程式作業步驟的屬性，或定義新的作業步驟。  
  
若要導覽至此頁面，請在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 物件總管中，展開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent，以滑鼠右鍵按一下 [作業]，按一下 [新增作業]，選取 [步驟] 頁面，然後按一下 [新增]。 您也可用滑鼠右鍵按一下物件總管中的作業，按一下 [屬性]、選取 [步驟] 頁面，然後按一下 [新增]、[插入] 或 [編輯]，以導覽至此頁面。  
  
## <a name="options"></a>選項。  
**步驟名稱**  
設定作業步驟的名稱。  
  
**型別**  
設定作業步驟使用的子系統。 根據您選擇的子系統，會顯示定義作業步驟變更的選項。  
  
**執行身分**  
設定作業步驟的 Proxy 帳戶。 系統管理員 (sysadmin) 固定伺服器角色的成員也會指定 [SQL 代理程式服務帳戶]。  
  
**資料庫**  
設定作業步驟執行所在的資料庫。 並非所有作業步驟類型都可使用這個選項。  
  
**Command**  
設定作業步驟執行的命令。  
  
## <a name="options-for-transact-sql-job-steps"></a>Transact-SQL 作業步驟的選項  
**開啟**  
從檔案載入命令。  
  
**全選**  
選取命令的文字。  
  
**複製**  
將選取的文字複製到剪貼簿。  
  
**貼上**  
貼上剪貼簿的內容。  
  
**剖析**  
檢查命令的語法。  
  
## <a name="options-for-activex-script-job-steps"></a>ActiveX 指令碼作業步驟的選項  
  
> [!IMPORTANT]  
> 將從未來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 版本的 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Agent 中移除 ActiveX Scripting 子系統。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
**VBScript**  
指定 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Basic Scripting Edition 做為作業步驟的語言。  
  
**JScript**  
指定 JScript 做為作業步驟的語言。  
  
**其他**  
輸入以另一種指令碼語言撰寫之作業步驟的語言名稱。  
  
**開啟**  
從檔案載入命令。  
  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>作業系統 (CmdExec) 作業步驟的選項  
**成功命令的處理序結束碼**  
輸入命令傳回表示成功的結束碼。  
  
**開啟**  
從檔案載入命令。  
  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-powershell-job-steps"></a>PowerShell 作業步驟的選項  
**開啟**  
從檔案載入指令碼。  
  
**全選**  
選取指令碼的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-replication-distributor-job-steps"></a>複寫散發者作業步驟的選項  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-replication-merge-job-steps"></a>複寫合併作業步驟的選項  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>複寫佇列讀取器作業步驟的選項  
**資料庫**  
作業步驟將使用的資料庫。  
  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-replication-snapshot-job-steps"></a>複寫快照集作業步驟的選項  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-replication-transaction-log-reader-job-steps"></a>複寫交易記錄讀取器作業步驟的選項  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-sql-server-analysis-services-command-job-steps"></a>SQL Server Analysis Services 命令作業步驟的選項  
**Server**  
選取作業步驟執行所在的伺服器。  
  
**開啟**  
從檔案載入命令。  
  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-sql-server-analysis-services-query-job-steps"></a>SQL Server Analysis Services 查詢作業步驟的選項  
**Server**  
選取作業步驟執行所在的伺服器。  
  
**資料庫**  
作業步驟將使用的資料庫。  
  
**開啟**  
從檔案載入命令。  
  
**全選**  
選取命令的文字。  
  
**複製**  
複製選取的文字。  
  
**貼上**  
貼上剪貼簿的內容。  
  
## <a name="options-for-integration-services-package-execution-job-steps"></a>Integration Services 封裝執行作業步驟的選項  
  
### <a name="general-tab"></a>General Tab  
指定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] ([!INCLUDE[ssIS](../../includes/ssis_md.md)]) 封裝所在的位置，以及要使用何種驗證方法。 當您選取這個索引標籤時，可以使用下列選項。  
  
**封裝來源**  
指定儲存 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝的位置。 選擇下列其中之一：  
  
-   **SQL Server**  
  
-   **檔案系統**  
  
-   **SSIS 封裝存放區**  
  
**Server**  
輸入儲存 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝的伺服器名稱。 唯有當 [套件來源] 指定 [SQL Server] 或 [SSIS 套件存放區] 時，才能使用此選項。  
  
**使用 Windows 驗證**  
使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Windows 驗證登入 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 。  
  
**使用 SQL Server 驗證**  
使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 。 如果選取這種驗證方法，請輸入適當的 [使用者名稱] 和 [密碼]。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 提供驗證的目的在提供回溯相容性。 為了提升安全性，如果可能的話請使用 Windows 驗證。  
  
**封裝**  
輸入封裝的位置。  
  
> [!IMPORTANT]  
> 對於受密碼保護的 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 套件，按一下 [組態] 索引標籤，在 [套件密碼] 對話方塊中輸入密碼。 否則，執行受密碼保護之封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業將會失敗。  
  
### <a name="configurations-tab"></a>組態索引標籤  
指定 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝的組態選項。 當選取這個索引標籤時，可以使用下列選項。  
  
**組態檔**  
列出封裝的組態檔。  
  
**加入**  
加入封裝的組態檔。  
  
**移除**  
移除封裝的組態檔。  
  
**上移**  
將選取的組態檔上移。  
  
**下移**  
將選取的組態檔下移。  
  
### <a name="command-files-tab"></a>命令檔索引標籤  
選取封裝的命令檔。 依命令檔在清單中出現的順序處理命令檔。 當您選取這個索引標籤時，可以使用下列選項。  
  
**命令檔**  
列出封裝的命令檔。  
  
**加入**  
加入命令檔。  
  
**移除**  
移除選取的命令檔。  
  
**上移**  
將選取的命令檔上移。  
  
**下移**  
將選取的命令檔下移。  
  
### <a name="data-sources-tab"></a>資料來源索引標籤  
檢視在此索引標籤上之封裝中所指定的資料來源。  
  
**連線管理員**  
檢視資料來源的名稱。  
  
**說明**  
檢視資料來源的描述。  
  
**連接字串**  
檢視資料來源的連接字串。  
  
### <a name="execution-options-tab"></a>執行選項索引標籤  
檢視或變更在此索引標籤上之封裝的執行選項。  
  
**發生驗證警告時封裝就失敗**  
如果發生驗證警告時要使封裝執行失敗，請選取此選項。  
  
**驗證封裝但不執行**  
作業步驟要驗證但不執行封裝時，請選取此選項。  
  
**最大並行可執行檔數目**  
可以同時執行的最大可執行檔數目。  
  
**啟用封裝檢查點**  
作業步驟要使用封裝檢查點時，請選取此選項。  
  
**檢查點檔案**  
輸入封裝檢查點檔案的名稱。  
  
**...**  
瀏覽以尋找封裝檢查點檔案。  
  
**覆寫重新啟動選項**  
若要為此作業步驟指定不同於封裝中所指定的重新啟動選項時，請選取此選項。  
  
**重新啟動選項**  
選取封裝重新啟動時要採取的動作。  
  
### <a name="logging-tab"></a>記錄索引標籤  
檢視或變更在此索引標籤上之封裝的記錄提供者。  
  
**記錄提供者**  
選取記錄提供者的 ClassID。  
  
**組態字串**  
輸入記錄提供者的組態字串。  
  
**移除**  
移除記錄提供者。  
  
### <a name="set-values-tab"></a>設定值索引標籤  
檢視或變更在此索引標籤上之封裝的屬性值。  
  
**屬性路徑**  
檢視或變更屬性的路徑。  
  
**Value**  
檢視或變更屬性的值。  
  
**移除**  
移除屬性。  
  
### <a name="verification-tab"></a>驗證索引標籤  
選取在此索引標籤上之作業步驟的驗證選項。  
  
**只執行簽署的封裝**  
只執行已經簽署的封裝。 選取此選項時，如果封裝未簽署，作業步驟就會失敗。  
  
**確認封裝組建**  
只執行具有特定組建編號的封裝。 選取此選項時，如果封裝沒有指定的組建編號，作業步驟就會失敗。  
  
**建置**  
輸入封裝的組建編號。  
  
**確認封裝識別碼**  
只執行具有特定識別碼的封裝。 選取此選項時，如果封裝沒有指定的識別碼，作業步驟就會失敗。  
  
**封裝識別碼**  
輸入封裝識別碼。  
  
**確認版本識別碼**  
只執行具有特定版本識別碼的封裝。 選取此選項時，如果封裝沒有指定的版本識別碼，作業步驟就會失敗。  
  
**版本識別碼**  
輸入版本識別碼。  
  
### <a name="command-line-tab"></a>命令列索引標籤  
指定封裝的命令列選項。 當選取這個索引標籤時，可以使用下列選項。  
  
**還原原始選項**  
使用此對話方塊中所設定的命令列選項。  
  
**手動編輯命令列**  
指定命令列視窗中的選項。  
  
**命令列**  
輸入此封裝所用的命令列選項。  
  
## <a name="see-also"></a>另請參閱  
[管理作業步驟](../../ssms/agent/manage-job-steps.md)  
[封裝的 SQL Server Agent 作業](http://msdn.microsoft.com/en-us/ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31)  
[管理複寫代理程式](http://msdn.microsoft.com/en-us/f27186b8-b1b2-4da0-8b2b-91f632c2ab7e)  
  
