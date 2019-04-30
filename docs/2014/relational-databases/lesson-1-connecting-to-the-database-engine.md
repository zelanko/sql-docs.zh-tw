---
title: 第 1 課：連線到資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 32b78c210647ab5b3722f01f334e9cb2e8bbfc13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63145509"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>第 1 課：連線到資料庫引擎
  當您安裝 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]時，所安裝的工具視版本和安裝選項而定。 這一課檢閱主要工具，顯示您如何連接及執行基本功能 (授權更多使用者)。  
  
  
  
##  <a name="tools"></a> 使用者入門的工具  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 出貨時已附帶各種工具。 這個主題描述您需要的優先工具，並幫助您選取作業的正確工具。 所有工具都可以從 [開始] 功能表存取。 根據預設，有些工具 (像是 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]) 並不會安裝。 您必須在安裝期間選取工具作為用戶端元件的一部分。 如需下面所述工具的完整描述，請在《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中搜尋相關內容。 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 只包含工具的子集。  
  
### <a name="basic-tools"></a>基本工具  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是管理 [!INCLUDE[ssDE](../includes/ssde-md.md)] 及撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 程式碼的主要工具。 它裝載於 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Shell 中， 它不會納入[!INCLUDE[ssExpress](../includes/ssexpress-md.md)]，但可從個別下載，其中包括[Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=144346)。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員會隨著 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和用戶端工具一起安裝。 它可讓您啟用伺服器通訊協定、設定通訊協定選項 (例如 TCP 通訊埠)、設定伺服器服務自動啟動，以及設定用戶端電腦以您偏好的方式連接。 這個工具會設定更進階的連接元素，但是不會啟用功能。  
  
### <a name="sample-database"></a>範例資料庫  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]未隨附範例資料庫和範例。 《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中所描述的大多數範例都是使用 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 範例資料庫。  
  
##### <a name="to-start-sql-server-management-studio"></a>啟動 SQL Server Management Studio  
  
-   在上**開始**功能表上，指向**所有程式**，指向[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]，然後按一下**SQL Server Management Studio**。  
  
##### <a name="to-start-sql-server-configuration-manager"></a>啟動 SQL Server 組態管理員  
  
-   指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
##  <a name="connect"></a> 連接 Management Studio  
 如果您知道執行個體的名稱，而且是以電腦上管理員群組的成員身分來連接，則要從相同電腦上所執行的工具連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 很容易。 下列程序必須執行在主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的相同電腦上。  
  
##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>判斷 Database Engine 執行個體的名稱  
  
1.  以系統管理員群組的成員身分登入 Windows，然後開啟 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
    > [!IMPORTANT]  
    >  如果您要連接到[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]上[!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]或[!INCLUDE[nextref_longhorn](../includes/nextref-longhorn-md.md)]（或較新），您可能需要以滑鼠右鍵按一下[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，然後按一下 **系統管理員身分執行**才能使用您的系統管理員進行連接認證。 從 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 開始，安裝程式會將選取的登入加入至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，因此不需要您的系統管理員認證。  
  
2.  在 [連接到伺服器] 對話方塊中，按一下 [取消]。  
  
3.  如果未顯示 [已註冊的伺服器]，請在 [檢視] 功能表上按一下 [已註冊的伺服器]。  
  
4.  在 [已註冊的伺服器] 工具列上選取 [Database Engine] 之後，展開 [Database Engine]、以滑鼠右鍵按一下 [本機伺服器群組]、指向 [工作]，然後按一下 [註冊本機伺服器]。 此時會顯示電腦上已安裝的所有 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體。 預設的執行個體未命名，而是以電腦名稱顯示。 具名執行個體是顯示為電腦名稱，後面接著反斜線 (\\) 和執行個體名稱。 若為 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]，除非在安裝期間變更名稱，否則執行個體是命名為 *<computer_name>* \sqlexpress。  
  
##### <a name="to-verify-that-the-database-engine-is-running"></a>確認 Database Engine 是否在執行中  
  
1.  在 [已註冊的伺服器] 中，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的名稱旁邊有一個綠點和白色箭頭，表示 [!INCLUDE[ssDE](../includes/ssde-md.md)] 在執行中，不需要進一步動作。  
  
2.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體的名稱旁邊有一個紅點和白色方塊，表示 [!INCLUDE[ssDE](../includes/ssde-md.md)] 已停止。 以滑鼠右鍵按一下 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的名稱，並按一下 [服務控制]，然後按一下 [啟動]。 在確認對話方塊之後，[!INCLUDE[ssDE](../includes/ssde-md.md)] 應該已經啟動，而且圓圈會變成帶有白色箭頭的綠色圖示。  
  
##### <a name="to-connect-to-the-database-engine"></a>連接到 Database Engine  
  
1.  在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中，按一下 [檔案] 功能表上的 [連接物件總管]。  
  
     [連接到伺服器] 對話方塊隨即開啟。 [伺服器類型] 方塊會顯示上次使用的元件類型。  
  
2.  選取 [Database Engine]。  
  
3.  在 [伺服器名稱] 方塊中，輸入 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體的名稱。 若為 SQL Server 的預設執行個體，則伺服器名稱為電腦名稱。 若為 SQL Server 的具名執行個體，則伺服器名稱為 <電腦名稱>****\\<執行個體名稱>****，例如 **ACCTG_SRVR\SQLEXPRESS**。  
  
4.  按一下 **[連接]**。  
  
##  <a name="additional"></a> 授權其他連線  
 既然您以管理員身分連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，您的首要工作之一就是授權其他使用者連接。 您可以建立登入，並授權該登入以使用者身分存取資料庫，來達成此目的。 登入可以是使用 Windows 認證的 Windows 驗證登入，或是 SQL Server 驗證登入，這種登入會將驗證資訊儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，而且與 Windows 認證無關。 可能的話，請盡量使用 Windows 驗證。  
  
##### <a name="create-a-windows-authentication-login"></a>建立 Windows 驗證登入  
  
1.  在上一項工作中，您使用 [!INCLUDE[ssDE](../includes/ssde-md.md)] 連接到 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 在物件總管中，展開伺服器執行個體，展開 [安全性]，以滑鼠右鍵按一下 [登入]，然後按一下 [新增登入]。  
  
     [登入 - 新增] 對話方塊隨即出現。  
  
2.  在 **一般**頁面上，於**登入名稱**方塊中，輸入下列格式的 Windows 登入*\<網域 >\\< 登入\>*。  
  
3.  在 [預設資料庫] 方塊中，選取 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] (如果有的話)。 否則，請選取 [master]。  
  
4.  在 [伺服器角色] 頁面上，如果新登入將成為管理員，請按一下 [系統管理員 (sysadmin)]，否則保留空白。  
  
5.  在 [使用者對應] 頁面上，對 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫選取 [對應] \(如果有的話)。 否則，請選取 [master]。 請注意，[使用者] 方塊會填入此登入。 當此對話方塊關閉時，會在資料庫中建立此使用者。  
  
6.  在 [預設結構描述] 方塊中輸入 **dbo**，將登入對應到資料庫擁有者結構描述。  
  
7.  接受 [安全性實體] 和 [狀態] 方塊的預設值，並按一下 [確定] 來建立登入。  
  
> [!IMPORTANT]  
>  這是讓您快速入門的基本資訊。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供多樣化的安全性環境，安全性顯然是資料庫作業的重要一環。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：從另一部電腦連線](lesson-2-connecting-from-another-computer.md)  
  
  
