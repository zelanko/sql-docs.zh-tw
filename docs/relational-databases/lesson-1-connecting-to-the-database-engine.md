---
title: "第 1 課：連接到資料庫引擎 | Microsoft Docs"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: efa0929341a017bb82136a84427a32118167c504
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-connecting-to-the-database-engine"></a>第 1 課：連接到 Database Engine
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

當您安裝 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]時，所安裝的工具視版本和安裝選項而定。 這一課檢閱主要工具，顯示您如何連接及執行基本功能 (授權更多使用者)。  
  
這一課包含下列工作：  
  
-   [使用者入門的工具](#tools)  
  
-   [連接 Management Studio](#connect)  
  
-   [授權其他連接](#additional)  
  
## <a name="tools"></a>使用者入門的工具  
[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 出貨時已附帶各種工具。 這個主題描述您需要的優先工具，並幫助您選取作業的正確工具。 所有工具都可以從 [開始] 功能表存取。 根據預設，有些工具 (像是 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]) 並不會安裝。 您必須在安裝期間選取工具作為用戶端元件的一部分。 如需下面所述工具的完整描述，請在《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中搜尋相關內容。 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 只包含工具的子集。  
  
### <a name="basic-tools"></a>基本工具  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) 是管理 [!INCLUDE[ssDE](../includes/ssde-md.md)] 以及撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 程式碼的主要工具。 它裝載於 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Shell 中， 您可以從 [Microsoft 下載中心](https://msdn.microsoft.com/library/mt238290.aspx)免費下載 SSMS。 最新版本可以與舊版 [!INCLUDE[ssDE_md](../includes/ssde-md.md)]搭配使用。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員會隨著 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和用戶端工具一起安裝。 它可讓您啟用伺服器通訊協定、設定通訊協定選項 (例如 TCP 通訊埠)、設定伺服器服務自動啟動，以及設定用戶端電腦以您偏好的方式連接。 這個工具會設定更進階的連接元素，但是不會啟用功能。  
  
### <a name="sample-database"></a>範例資料庫  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]未隨附範例資料庫和範例。 《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中所描述的大多數範例都是使用 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 範例資料庫。  
  
##### <a name="to-start-sql-server-management-studio"></a>啟動 SQL Server Management Studio  
  
- 在目前的 Windows 版本上，於 [開始] 頁面上輸入 SSMS，然後按一下 [Microsoft SQL Server Management Studio]。  
-   使用舊版 Windows 時，請在 [開始] 功能表上依序指向 [所有程式] 和 [[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]]，然後按一下 [SQL Server Management Studio]。  
  
##### <a name="to-start-sql-server-configuration-manager"></a>啟動 SQL Server 組態管理員  
  
- 在目前的 Windows 版本上，於 [開始] 頁面上輸入**組態管理員**，然後按一下 [SQL Server *版本*組態管理員]。   
-   使用舊版 Windows 時，請在 [開始] 功能表上依序指向 [所有程式]、[[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]] 和 [組態工具]，然後按一下 [SQL Server 組態管理員]。  
  
## <a name="connect"></a>連接 Management Studio  
如果您知道執行個體的名稱，而且是以電腦上本機系統管理員群組的成員身分來連接，則要從相同電腦上所執行的工具連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 很容易。 下列程序必須執行在主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的相同電腦上。  
  
> [!NOTE]  
> 本主題討論如何連接至內部部署 SQL Server。 若要連接到 Azure SQL Database，請參閱 [使用 SQL Server Management Studio 連接到 SQL Database 並執行範例 T-SQL 查詢](https://azure.microsoft.com/documentation/articles/sql-database-connect-query-ssms/)。  
  
##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>判斷 Database Engine 執行個體的名稱  
  
1.  以系統管理員群組的成員身分登入 Windows，然後開啟 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
2.  在 [連接到伺服器] 對話方塊中，按一下 [取消]。  
  
3.  如果未顯示 [已註冊的伺服器]，請在 [檢視] 功能表上按一下 [已註冊的伺服器]。  
  
4.  在 [已註冊的伺服器] 工具列上選取 [Database Engine] 之後，展開 [Database Engine]、以滑鼠右鍵按一下 [本機伺服器群組]、指向 [工作]，然後按一下 [註冊本機伺服器]。 此時會顯示電腦上已安裝的所有 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體。 預設的執行個體未命名，而是以電腦名稱顯示。 具名執行個體是顯示為電腦名稱，後面接著反斜線 (\\) 和執行個體名稱。 若為 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]，除非在安裝期間變更名稱，否則執行個體是命名為 *<computer_name>*\sqlexpress。  
  
##### <a name="to-verify-that-the-database-engine-is-running"></a>確認 Database Engine 是否在執行中  
  
1.  在 [已註冊的伺服器] 中，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的名稱旁邊有一個綠點和白色箭頭，表示 [!INCLUDE[ssDE](../includes/ssde-md.md)] 在執行中，不需要進一步動作。  
  
2.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體的名稱旁邊有一個紅點和白色方塊，表示 [!INCLUDE[ssDE](../includes/ssde-md.md)] 已停止。 以滑鼠右鍵按一下 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的名稱，並按一下 [服務控制]，然後按一下 [啟動]。 在確認對話方塊之後，[!INCLUDE[ssDE](../includes/ssde-md.md)] 應該已經啟動，而且圓圈會變成帶有白色箭頭的綠色圖示。  
  
##### <a name="to-connect-to-the-database-engine"></a>連接到 Database Engine  

安裝 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 時，選取至少一個系統管理員帳戶。 以系統管理員身分登入 Windows 時，請執行下列步驟。
  
1.  在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中，按一下 [檔案] 功能表上的 [連接物件總管]。  
  
    [連接到伺服器] 對話方塊隨即開啟。 [伺服器類型] 方塊會顯示上次使用的元件類型。  
  
2.  選取 [Database Engine]。  

    ![object-explorer](../relational-databases/media/object-explorer.png)
  
3.  在 [伺服器名稱] 方塊中，輸入 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體的名稱。 若為 SQL Server 的預設執行個體，則伺服器名稱為電腦名稱。 若為 SQL Server 的具名執行個體，則伺服器名稱為 *<電腦名稱>***\\***<執行個體名稱>*，例如 **ACCTG_SRVR\SQLEXPRESS**。 下列螢幕擷取畫面會顯示連接至名為 'PracticeComputer' 之電腦上的預設 (未命名) [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 執行個體。 登入 Windows 的使用者是來自 Contoso 網域的 Mary。 使用 Windows 驗證時，即無法變更使用者名稱。 

    ![connect-to-server](../relational-databases/media/connect-to-server.png)
  
4.  按一下 **[連接]**。  

> [!NOTE]
> 本教學課程假設您不熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 而且沒有特殊連接問題。 這應該適用於大部分的人，並且保持本教學課程的簡單性。 如需詳細疑難排解步驟，請參閱 [針對 SQL Server Database Engine 的連接進行疑難排解](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。 
  
## <a name="additional"></a>授權其他連接  
既然您以管理員身分連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，您的首要工作之一就是授權其他使用者連接。 您可以建立登入，並授權該登入以使用者身分存取資料庫，來達成此目的。 登入可以是使用 Windows 認證的 Windows 驗證登入，或是 SQL Server 驗證登入，這種登入會將驗證資訊儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，而且與 Windows 認證無關。 可能的話，請盡量使用 Windows 驗證。

> [!TIP]
> 大部分的組織都有網域使用者，並使用 Windows 驗證。 您可以在電腦上建立其他本機使用者來自行進行實驗。 將透過您的電腦驗證本機使用者，因此網域是電腦名稱。 例如，如果您的電腦命名為 `MyComputer` ，並且建立名為 `Test`的使用者，則使用者的 Windows 描述是 `Mycomputer\Test`。  
  
##### <a name="create-a-windows-authentication-login"></a>建立 Windows 驗證登入  
  
1.  在上一項工作中，您使用 [!INCLUDE[ssDE](../includes/ssde-md.md)] 連接到 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 在物件總管中，展開伺服器執行個體，展開 [安全性]，以滑鼠右鍵按一下 [登入]，然後按一下 [新增登入]。  
  
    [登入 - 新增] 對話方塊隨即出現。  
  
2.  在 [一般] 頁面的 [登入名稱] 方塊中，以下列格式輸入 Windows 登入：`<domain>\\<login>`
  
    ![new-login](../relational-databases/media/new-login.png)
  
3.  在 [預設資料庫] 方塊中，選取 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] (如果有的話)。 否則，請選取 [master]。  
  
4.  在 [伺服器角色] 頁面上，如果新登入將成為管理員，請按一下 [系統管理員 (sysadmin)]，否則保留空白。  
  
5.  在 [使用者對應] 頁面上，對 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫選取 [對應] (如果有的話)。 否則，請選取 [master]。 請注意，[使用者] 方塊會填入此登入。 當此對話方塊關閉時，會在資料庫中建立此使用者。  
  
6.  在 [預設結構描述] 方塊中輸入 **dbo**，將登入對應到資料庫擁有者結構描述。  
  
7.  接受 [安全性實體] 和 [狀態] 方塊的預設值，並按一下 [確定] 來建立登入。  
  
> [!IMPORTANT]  
> 這是讓您快速入門的基本資訊。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供多樣化的安全性環境，安全性顯然是資料庫作業的重要一環。  
  
## <a name="next-lesson"></a>下一課  
[第 2 課：從另一部電腦連接](../relational-databases/lesson-2-connecting-from-another-computer.md)  
  
  
  


