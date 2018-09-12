---
title: 疑難排解 SQL Server 公用程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f5f47c2a-38ea-40f8-9767-9bc138d14453
caps.latest.revision: 8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d059ac17d901ca7eec0bf451ba7babaecce607a8
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815744"
---
# <a name="troubleshoot-the-sql-server-utility"></a>疑難排解 SQL Server 公用程式
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式問題的疑難排解可能包括解決 SQL Server 執行個體向 UCP 註冊作業失敗的問題、解決因無法收集資料而導致 UCP 上 Managed 執行個體清單檢視變為灰色圖示的問題、改善效能瓶頸或是解決資源健全狀況的問題。 如需有關所識別的資源健全狀況問題的緩和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]UCP，請參閱 <<c2> [ 疑難排解的 SQL Server 資源健全狀況&#40;SQL Server 公用程式&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)。</c2>  
  
## <a name="failed-operation-to-enroll-an-instance-of-sql-server-into-a-sql-server-utility"></a>SQL Server 執行個體向 SQL Server 公用程式註冊的作業失敗  
 如果您連接到執行個體[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]註冊使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]驗證，以及您指定的 proxy 帳戶，屬於 UCP 所在網域不同的 Active Directory 網域執行個體驗證成功，但註冊作業會失敗並出現下列錯誤訊息：  
  
 執行 Transact-SQL 陳述式或批次時發生例外狀況。 (Microsoft.SqlServer.ConnectionInfo)  
  
 其他資訊: 無法獲得關於 Windows NT 群組/使用者 '\<域名稱\帳戶名稱>' 的資訊，錯誤碼 0x5。 (Microsoft SQL Server，錯誤：15404)  
  
 這個問題可能會在下列範例狀況中發生：  
  
1.  UCP 為 "Domain_1" 的成員。  
  
2.  目前使用的是單向網域信任關係：換言之，"Domain_1" 並不受到 "Domain_2" 信任，但是 "Domain_2" 已受到 "Domain_1" 信任。  
  
3.  要註冊到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體也是 "Domain_1" 的成員。  
  
4.  在註冊期間，使用 “sa” 連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。 指定 "Domain_2" 的 Proxy 帳戶。  
  
5.  驗證會成功，但是註冊會失敗。  
  
 若以上述範例而言，解決這個問題的辦法是使用 “sa” 連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體來向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式註冊，並且提供 "Domain_1" 的 Proxy。  
  
## <a name="failed-wmi-validation"></a>WMI 驗證失敗  
 如果沒有在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體上正確設定 WMI，那麼 [建立 UCP] 與 [註冊受管理的執行個體] 作業會顯示警告，但是並不會封鎖作業。 此外，如果您變更[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理程式帳戶設定，讓[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理程式沒有存取必要 WMI 類別，在受影響的受控執行個體的資料集合的權限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]無法上傳到 UCP。 如此會造成 UCP 中顯示灰色圖示。  
  
 對於受影響的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 受管理的執行個體，失敗的資料收集會造成 UCP 清單檢視中出現灰色狀態圖示。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 受管理的執行個體中的作業記錄指出 sysutility_mi_collect_and_upload 在步驟 2 失敗 (從 PowerShell 指令碼收集的階段資料)。  
  
 簡化的錯誤訊息如下：  
  
 命令執行已停止因為 Shell 變數 "ErrorActionPreference" 已設定為 [停止: 拒絕存取]。  
  
 錯誤：\<日期-時間 （MM/DD/YYYY hh: mm:） >： 收集 cpu 屬性時例外狀況。  WMI 查詢可能已經失敗。  警告。  
  
 若要解決這個問題，請確認下列組態設定：  
  
-   在 Windows Server 2003 上的 SQL Server Agent 服務必須是受管理的執行個體的 Windows 效能監視器使用者群組的一部分[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   WMI 服務必須在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 受管理的執行個體上啟用與設定。  
  
-   WMI 存放庫可能會損毀的受管理的執行個體上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   效能程式庫可能會遺失或損毀的受管理的執行個體上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
 若要確認特定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體是否已適當設定為會回報資料給 UCP，請確認下列類別可以在特定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上使用，而且 SQL Server Agent 服務帳戶可以存取這些類別：  
  
-   Win32_MountPoint  
  
-   Win32_PerfRawData_PerfProc_Process  
  
-   Win32_PerfRawData_PerfOS_Processor  
  
-   Win32_Processor  
  
-   Win32_Volume  
  
-   Win32_LogicalDisk  
  
 您可以在每一個類別上使用 Get-WmiObject PowerShell 指令程式，藉此確認是可以存取每一個類別。 受控執行個體上執行下列 cmdlet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
```  
Get-WmiObject Win32_MountPoint -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_PerfRawData_PerfProc_Process -ErrorAction Stop| Out-Null  
Get-WmiObject Win32_PerfRawData_PerfOS_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Volume -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_LogicalDisk -ErrorAction Stop | Out-Null  
```  
  
 如需有關疑難排解 WMI 的詳細資訊，請參閱 <<c0> [ 疑難排解 WMI](http://go.microsoft.com/fwlink/?LinkId=178250)。 請注意，這些 SQL Server 公用程式作業中的查詢會於本機執行，因此，無法適用 DCOM 與遠端疑難排解內容。  
  
## <a name="failed-data-collection"></a>資料收集失敗  
 如果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]公用程式資料收集事件失敗，請考慮下列可能性：  
  
-   請勿在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 受管理的執行個體上變更「公用程式資訊」收集組的任何屬性，也請勿手動開啟/關閉資料收集，因為資料收集是由公用程式代理程式作業所控制。  
  
-   WMI 驗證失敗或不受支援。 如需詳細資訊，請參閱本主題稍早的＜WMI 驗證失敗＞一節。  
  
-   在受管理的執行個體清單檢視中，資料重新整理中的資料[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]公用程式視點不會自動重新整理。 若要重新整理資料，請以滑鼠右鍵按一下**受控執行個體**中的節點**公用程式總管導覽**窗格中，然後選取**重新整理**，或以滑鼠右鍵按一下[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體名稱，在清單檢視中，然後選取**重新整理**。 請注意，當使用 UCP 註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體之後，最多需要 30 分鐘的時間，資料才會第一次出現在 [公用程式總管] 內容窗格的儀表板和視點內。  
  
-   使用 SQL Server 組態管理員來驗證執行個體[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在執行。  
  
-   如果資料收集或資料上傳因逾時問題而失敗，請更新 MSDB 資料庫中的 dbo.fn_sysutility_mi_get_collect_script() 函數。 特別是在 "Invoke-BulkCopyCommand()" 函數中加入下一行：  
  
    ```  
    $bulkCopy.BulkCopyTimeout=180  
    ```  
  
     預設的逾時值是 30 秒。  
  
-   如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體尚未叢集化，請確認 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務正在執行中，而且此服務在 UCP 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 Managed 執行個體上設定為自動啟動。  
  
-   驗證有效的帳戶時所使用的受管理的執行個體上執行資料收集[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 例如，密碼可能已過期。 如果 Proxy 密碼已經過期，請在 SSMS 中更新密碼認證，如下所示：  
  
    1.  在 SSMS 的 **[物件總管]** 中，展開 **[安全性]** 節點，然後展開 **[認證]** 節點。  
  
    2.  以滑鼠右鍵按一下**UtilityAgentProxyCredential_\<GUID >** ，然後選取**屬性**。  
  
    3.  在 [認證屬性] 對話方塊中，更新為所需的認證**UtilityAgentProxyCredential_\<GUID >** 認證。  
  
    4.  按一下 **[確定]** 以確認變更。  
  
-   應該啟用 TCP/IP 的受管理的執行個體和 UCP 上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 啟用透過 TCP/IP [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager。  
  
-   您應該啟動 UCP 上的 SQL Server Browser 服務，並將它設定為自動啟動。 如果您的組織阻止使用 SQL Server Browser 服務，請使用下列步驟讓 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的受管理的執行個體連接到 UCP：  
  
    1.  在 Windows 工作列上的受管理的執行個體上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，按一下**開始**，然後按一下 **執行...**.  
  
    2.  在提供的空間內輸入 "cliconfg.exe"，然後按一下 **[確定]**。  
  
    3.  如果系統允許 SQL 用戶端組態公用程式 EXE 啟動，請按一下 **[繼續]**。  
  
    4.  在 **[SQL Server 用戶端網路公用程式]** 對話方塊中，選取 **[別名]** 索引標籤，然後按一下 **[加入]**。  
  
    5.  在 **[加入網路程式庫組態]** 對話方塊中：  
  
    6.  從網路程式庫清單中指定 TCP/IP。  
  
    7.  在 **[伺服器別名]** 文字方塊中指定 UCP 的 ComputerName\InstanceName。  
  
    8.  在 **[伺服器名稱]** 文字方塊中指定 UCP 的 ComputerName。  
  
    9. 取消核取 **[動態決定通訊埠]** 核取方塊。  
  
    10. 在 **[通訊埠編號]** 文字方塊中，指定 UCP 接聽的通訊埠編號。  
  
    11. 按一下 **[確定]** 儲存您的變更。  
  
    12. 針對每個受管理的執行個體重複這些步驟[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]連接至 UCP，其中未啟用 SQL Server Browser 服務。  
  
-   請確定管理的執行個體的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]連線到網路。  
  
-   如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的受管理的執行個體上有資料庫同名但是具有不同的區分大小寫設定，資料庫和它的視點之間的識別可能會不正確，因而導致資料收集失敗。 例如，名為 "MYDATABASE" 的資料庫可能會顯示名為 "MyDatabase" 之資料庫的健全狀態。 在這種情況下，不會產生任何錯誤。 資料收集失敗也可能是因為 UCP 中顯示的其他物件出現大小寫不符的情況，例如資料庫檔案與檔案群組名稱。  
  
-   如果在 Windows Server 2003 電腦上主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 受管理的執行個體，則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務帳戶必須屬於效能監視器使用者安全性群組或本機系統管理員群組。 否則，資料收集將會失敗，並產生拒絕存取錯誤。 若要新增[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理程式服務帳戶的效能監視器使用者安全性群組，請使用下列步驟：  
  
    1.  開啟 **[電腦管理]**，然後展開 **[本機使用者和群組]**，再展開 **[群組]**。  
  
    2.  以滑鼠右鍵按一下 **[效能監視器使用者]** ，然後選取 **[加入群組]**。  
  
    3.  按一下 **[加入]**。  
  
    4.  輸入用來執行 SQL Server Agent 服務的帳戶，然後按一下 **[確定]**。  
  
    5.  如果將使用者加入至這個群組之前，已經使用 UCP 註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，請重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [疑難排解 SQL Server 資源健全情況 &#40;SQL Server 公用程式&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)  
  
  
