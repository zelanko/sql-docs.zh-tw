---
title: "使用複製資料庫精靈 | Microsoft 文件"
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.cdw.packageconfiguration.f1
- sql13.swb.cdw.schedule.f1
- sql13.swb.cdw.transfermethod.f1
- sql13.swb.cdw.databases.f1
- sql13.swb.cdw.destinationconfiguration.f1
- sql13.swb.cdw.destination.f1
- sql13.swb.cdw.locationofsourcedbfiles.f1
- sql13.swb.cdw.source.f1
- sql13.swb.cdw.selectdatabaseobjects.f1
- sql13.swb.cdw.complete.f1
- sql13.swb.cdw.welcome.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
caps.latest.revision: "64"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7e53c91fb8462fb26fd5a94e20c7a6ba7e2f54d0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="use-the-copy-database-wizard"></a>使用複製資料庫精靈
[複製資料庫精靈] 可讓您輕鬆地將資料庫和特定伺服器物件，從某個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體移動或複製到另一個執行個體，而不需要讓伺服器停機。 使用此精靈可以執行下列作業： 
  
-   挑選來源和目的地伺服器。  
  
-   選取要移動或複製的資料庫。  
  
-   為資料庫指定檔案位置。  
  
-   將登入複製到目的地伺服器。  
  
-   複製其他支援的物件、作業、使用者定義的預存程序和錯誤訊息。  
  
-   排程何時要移動或複製資料庫。  
  

  
##  <a name="Restrictions"></a> 限制事項  
  
-   Express 版本不提供複製資料庫精靈。  
  
-   [複製資料庫精靈] 無法用於複製或移動下列資料庫：
  
    -   系統資料庫。
  
    -   標示為複寫的資料庫。
  
    -   標示為「無法存取」、「正在載入」、「離線」、「正在復原」、「有疑問」或是「緊急模式」的資料庫。
    
    -   在 Microsoft Azure 儲存體中儲存資料或記錄檔的資料庫。
  
-   您無法將資料庫移動或複製到舊版 SQL Server。
  
-   若您選取 **[移動]** 選項，則當移動資料庫之後，精靈會自動刪除來源資料庫。 如果您選取 **[複製]** 選項，「複製資料庫精靈」就不會刪除來源資料庫。  此外，選取的伺服器物件會複製到目的地，而不是移至目的地；唯一實際移動的物件是資料庫。
  
-   如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件方法來移動全文檢索目錄，您必須在移動之後重新擴展索引。  
  
-   **卸離與附加** 方法可卸離資料庫，移動或複製資料庫 .mdf、.ndf 和 .ldf 檔案，並在新的位置中重新附加資料庫。 對於 **卸離與附加** 方法而言，為了避免資料遺失或不一致，使用中工作階段不能附加到正在移動或複製的資料庫。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件方法而言，因為資料庫絕對不會離線，所以允許使用中工作階段。  

-    傳送參考目的地伺服器上還不存在之資料庫的 SQL Server Agent 作業，將會導致整個作業失敗。  此精靈會先嘗試建立 SQL Server Agent 作業，再建立資料庫。  因應措施：
     1. 在目的地伺服器上，建立與要複製或移動的資料庫名稱相同的 Shell 資料庫。  請參閱[建立資料庫](../../relational-databases/databases/create-a-database.md)。
     
     2. 從 [設定目的地資料庫] 頁面中，選取 [卸除目的地伺服器上具有相同名稱的資料庫，然後繼續資料庫傳送，並覆寫現有的資料庫檔案]。

> **重要！！** **卸離與附加**方法會使來源和目的地資料庫擁有權，成為設定為執行 [複製資料庫精靈] 的登入。  若要變更資料庫的擁有權，請參閱 [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md) 。
  
  
##  <a name="Prerequisites"></a> 必要條件  
-   確定目的地伺服器上已啟動 SQL Server Agent。  

-   確定可從目的地伺服器連接到來源伺服器上的資料和記錄檔目錄。

-   根據 **卸離與附加** 方法，目的地伺服器上必須有 SSIS 子系統的 SQL Server Agent Proxy，以及可存取來源和目的地伺服器之檔案系統的認證。 如需 Proxy 的詳細資訊，請參閱 [建立 SQL Server Agent Proxy](~/ssms/agent/create-a-sql-server-agent-proxy.md)。

> **重要！！** 根據 **卸離與附加** 方法，若未使用 Integration Services Proxy 帳戶，複製或移動程序將會失敗。  在某些情況下，來源資料庫將無法重新附加至來源伺服器，並將從資料和記錄檔中移除所有 NTFS 安全性權限。  如果發生此情況，請巡覽至您的檔案、重新套用相關的權限，再將資料庫重新附加至您的 SQL Server 執行個體。
  
##  <a name="Recommendations"></a> 建議  
  
-   為了確保升級的資料庫能有最佳效能，請針對升級的資料庫執行 [sp_updatestats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) (更新統計資料)。  
  
-   將資料庫移動或複製到另一個伺服器執行個體時，為了提供使用者和應用程式的一致體驗，您可能必須在另一個伺服器執行個體上，為資料庫重新建立部分或所有中繼資料，例如登入和作業。 如需詳細資訊，請參閱[在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。  
  

  
###  <a name="Permissions"></a> Permissions  
 您必須在來源伺服器與目的地伺服器上成為 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
##  <a name="Overview"></a> [複製資料庫精靈] 頁面 
從 SQL Server Management Studio 的物件總管啟動 [複製資料庫精靈]，然後展開 [資料庫]。  以滑鼠右鍵按一下資料庫，指向 [工作]，然後按一下 [複製資料庫]。  如果出現 [歡迎使用複製資料庫精靈] 開頭顯示頁面，請按一下 [下一步]。


### <a name="select-a-source-server"></a>選取來源伺服器
用來指定要移動或複製之資料庫所在的伺服器，以及輸入登入資訊。  在您選取驗證方法並輸入登入資訊之後，按 **[下一步]** 以建立與來源伺服器的連接。  在整個工作階段中，此連接會保持開啟。

-    **來源伺服器**  
用來識別您要移動或複製之資料庫所在的伺服器名稱。  手動輸入，或按一下省略符號以巡覽至所需的伺服器。  該伺服器必須至少為 SQL Server 2005。

-    **使用 Windows 驗證**  
可讓使用者透過 Microsoft Windows 使用者帳戶連接。

-    **使用 SQL Server 驗證**  
可讓使用者經由提供 SQL Server 驗證使用者名稱和密碼來進行連接。

     -    **使用者名稱**  
用來輸入要連接的使用者名稱。 只有在您選擇使用 [SQL Server 驗證] 進行連接時，才能使用此選項。

     -    **密碼**  
用來輸入登入的密碼。 只有在您選擇使用 [SQL Server 驗證] 進行連接時，才能使用此選項。

###  <a name="select-a-destination-server"></a>選取目的地伺服器
用來指定要移動或複製資料庫的目的地伺服器。  如果您將來源和目的地伺服器設定成同一個伺服器執行個體，您就會建立一個資料庫複本。  在這種情況下，您必須稍後在精靈中重新命名此資料庫。  只有當目的地伺服器上沒有名稱衝突時，才可以將來源資料庫名稱用於複製或移動的資料庫。  如果有名稱衝突存在，您必須先手動解決目的地伺服器上的衝突，然後才能在這裡使用來源資料庫名稱。
  
-    **目的地伺服器**  
用來識別您要移動或複製資料庫的目的地伺服器名稱。  手動輸入，或按一下省略符號以巡覽至所需的伺服器。  該伺服器必須至少為 SQL Server 2005。

     >**注意：** 您可以使用屬於叢集伺服器的目的地。[複製資料庫精靈] 會確保您只能選取叢集目的地伺服器上的共用磁碟機。

-    **使用 Windows 驗證**  
可讓使用者透過 Microsoft Windows 使用者帳戶連接。

-    **使用 SQL Server 驗證**  
可讓使用者經由提供 SQL Server 驗證使用者名稱和密碼來進行連接。

     -    **使用者名稱**  
用來輸入要連接的使用者名稱。 只有在您選擇使用 [SQL Server 驗證] 進行連接時，才能使用此選項。

     -    **密碼**  
用來輸入登入的密碼。 只有在您選擇使用 [SQL Server 驗證] 進行連接時，才能使用此選項。

###  <a name="select-the-transfer-method"></a>選取傳送方法
 
-    **使用卸離和附加方法**  
從來源伺服器卸離資料庫，將資料庫檔案 (.mdf、.ndf 以及 .ldf) 複製到目的地伺服器，然後在目的地伺服器端附加該資料庫。 此方法通常是比較快速的方法，因為它的主要工作是讀取來源磁碟和寫入目的地磁碟。 不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 邏輯在資料庫中建立物件，或建立資料儲存結構。 不過，如果資料庫包含大量已配置但未使用的空間，此方法就會比較慢。 例如，新的且實際上幾乎是空的資料庫，在建立時若配置 100 MB，即使資料只填滿 5 MB，也會複製全部 100 MB。

     > **注意：** 此方法讓使用者在傳送期間無法使用資料庫。

     -    **如果失敗，則重新附加來源資料庫**  
     複製資料庫時，一律會將原始資料庫檔案重新附加至來源伺服器。 無法完成資料庫移動時，使用這個方塊即可將原始檔案重新附加至來源資料庫。 
  
-    **使用 SQL 管理物件方法**  
     這個方法會讀取來源資料庫上的每個資料庫物件的定義，然後在目的地資料庫中建立每個物件。 接著它會從來源資料表傳送資料到目的地資料表，重新建立索引與中繼資料。
  
     > [!NOTE]
     >  在傳送期間，資料庫使用者可以繼續存取資料庫。 
  
###  <a name="select-database"></a>選取資料庫
選取您要從來源伺服器移動或複製到目的地伺服器的資料庫。  請參閱主題上方的 [限制事項](#Restrictions) 。  
  
-    **[移動]**  
移動資料庫至目的地伺服器。

-    **[複製]**  
複製資料庫至目的地伺服器。

-    **Source**  
顯示存在於來源伺服器上的資料庫。

-    **狀態**  
顯示來源資料庫的各種資訊。

-    **重新整理**  
重新整理資料庫清單。
  
### <a name="configure-destination-database"></a>設定目的地資料庫
適當地變更資料庫名稱，以及指定資料庫檔案的位置和名稱。  每次移動或複製各個資料庫時，就會出現此頁面。

-    **來源資料庫**  
來源資料庫的名稱。  這是無法編輯的文字方塊。

-    **目的地資料庫**  
要建立的目的地資料庫名稱，請視需要進行修改。

-    **目的地資料庫檔案:**  
     
     -    **檔名**  
要建立的目的地資料庫檔案名稱，請視需要進行修改。

     -    **大小 (MB)**  
目的地資料庫檔案的大小 (以 MB 為單位)。

     -    **目的資料夾**  
要裝載目的地資料庫檔案之目的地伺服器上的資料夾，請視需要進行修改。

     -    **狀態**  
狀態

-    **如果目的地資料庫已存在:**  
     決定目的地資料庫已存在時所要採取的動作。

     -    **如果目的地已有相同名稱的資料庫或檔案，請停止傳送。**

     -    **卸除目的地伺服器上具有相同名稱的資料庫，然後繼續資料庫傳送，並覆寫現有的資料庫檔案。**

###  <a name="select-server-objects"></a>選取伺服器物件 
此頁面只能在來源和目的地是不同的伺服器時使用。  
  
-    **可用的相關物件**  
列出可傳送至目的地伺服器的物件。  若要包含物件，請按一下 [可用的相關物件] 方塊中的物件名稱，然後按一下 [>>] 按鈕，將物件移至 [選取的相關物件] 方塊。 

-    **選取的相關物件**  
列出將傳送至目的地伺服器的物件。  若要排除物件，請按一下 [選取的相關物件] 方塊中的物件名稱，然後按一下 [<\<] 按鈕，將物件移至 [可用的相關物件] 方塊。  根據預設，屬於所選取類型的所有物件都會傳送。 若要選擇任何類型的個別物件，請按一下 **[選取的相關物件]** 方塊中之任何物件類型旁的省略符號按鈕。  這會開啟一個對話方塊，其中您可以選取個別物件。

-    **伺服器物件清單** 

      -    **登入 (預設會選取)。** 
  
     -    **SQL Server Agent 作業**  
  
     -    **使用者自訂錯誤訊息**  
  
     -    **端點**  
  
     -    **全文檢索目錄** 
  
     -    **SSIS 封裝**  
     
     -    **master 資料庫裡的預存程序** 
          >**注意：** 擴充預存程序及其相關聯的 DLL 不適合自動複製。  
    
  
###   <a name="location-of-source-database-files"></a>來源資料庫檔案的位置
此頁面只能在來源和目的地是不同的伺服器時使用。  指定包含來源伺服器上之資料庫檔案的檔案系統共用。
  
-    **資料庫**  
     顯示要移動的每個資料庫的名稱。  
  
-    **資料夾位置**  
指定來源伺服器上之資料庫檔案的資料夾位置。
例如： `C:\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA`。

  
-    **來源伺服器上的檔案共用**  
包含來源伺服器上之資料庫檔案的檔案共用。  手動輸入共用，或按一下省略符號以巡覽至共用。
例如： `\\server_name\C$\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\Data`。

### <a name="configure-the-package"></a>設定套件
[複製資料庫精靈] 會建立 SSIS 封裝來傳送資料庫。

-    **封裝位置**  
顯示 SSIS 套件的寫入位置。

-    **封裝名稱**  
預設會建立 SSIS 封裝的名稱，請視需要進行修改。

-    **記錄選項**  
選取是要將記錄資訊儲存在 Windows 事件記錄檔中，還是儲存在文字檔中。

-    **錯誤記錄檔路徑**  
只有在已選取文字檔案登入選項時，才能使用此選項。  提供記錄檔位置的路徑。 

### <a name="schedule-the-package"></a>排程套件
指定您要開始進行移動或複製作業的時間。  如果您不是系統管理員，您必須指定可存取 Integration Services (SSIS) 封裝執行子系統的 SQL Server Agent Proxy 帳戶。

> **重要！！** Integration Services Proxy 帳戶必須依照 **卸離與附加** 方法使用。  

-    **立即執行**  
     完成精靈後將會執行 SSIS 封裝。
  
-    **排程**  
     根據排程來執行 SSIS 封裝。 
  
     -    **變更排程**   
開啟 [新增作業排程] 對話方塊。  請視需要進行設定。  完成後按一下 [確定]。


-    **Integration Services Proxy 帳戶**：從下拉式清單中選取可用的 Proxy 帳戶。  若要排程傳送，至少必須有一個 Proxy 帳戶可供使用者使用，而且帳戶要設定為擁有 **SSIS 封裝執行子系統**的權限。

        若要建立 SSIS 封裝執行的 Proxy 帳戶，請在物件總管中，依序展開 [SQL Server Agent] 和 [Proxy]，以滑鼠右鍵按一下 [SSIS 封裝執行]，然後按一下 [新增 Proxy]。

### <a name="complete-the-wizard"></a>完成精靈
顯示所選選項的摘要。  按 **[上一步]** 即可變更選項。  按一下 [完成] 以建立 SSIS 封裝。 [正在執行作業] 頁面會監視有關 [複製資料庫精靈] 執行的狀態資訊。

-    **動作**  
 列出每個執行的動作。

-    **狀態**  
 表示動作完全成功或失敗。

-    **訊息**  
提供每個步驟所傳回的任何訊息。

##  <a name="Examples"></a> 範例
### <a name="common-steps"></a>**通用步驟** 
不論您選擇的是 [移動] 或 [複製]、[卸離與附加] 或 [SMO]，下列五個步驟都會相同。  為求簡潔，這些步驟只會在此列出一次，所有範例將從**步驟 6** 開始進行。

1.  在物件總管中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。

2.  展開 [資料庫]，以滑鼠右鍵按一下所需的資料庫，指向 [工作]，然後按一下 [複製資料庫...]

3.  如果出現 [歡迎使用複製資料庫精靈] 開頭顯示頁面，請按一下 [下一步]。

4.  [選取來源伺服器] 頁面：指定要移動或複製之資料庫所在的伺服器。  選取驗證方法。  如果選擇 [使用 SQL Server 驗證]，則必須輸入您的登入認證。  按一下 [下一步]，建立與來源伺服器的連接。  在整個工作階段中，此連接會保持開啟。

5.  [選取目的地伺服器] 頁面：指定將移動或複製資料庫的目的地伺服器。  選取驗證方法。  如果選擇 [使用 SQL Server 驗證]，則必須輸入您的登入認證。  按一下 [下一步]，建立與來源伺服器的連接。  在整個工作階段中，此連接會保持開啟。

     > **注意：** 您可以從任何資料庫啟動 [複製資料庫精靈]。  您可以從來源或目的地伺服器使用 [複製資料庫精靈]。
  
### <a name="a--move-database-using-detach-and-attach-method-to-an-instance-on-a-different-physical-server--a-login-and-sql-server-agent-job-will-be-moved-as-well"></a>**A.使用卸離與附加方法，將資料庫移至不同實體伺服器上的執行個體。登入和 SQL Server Agent 作業也會一併移動。**  
下列範例會將 `Sales` 資料庫、名為 `contoso\Jennie` 的 Windows 登入和名為 `Jennie’s Report` 的 SQL Server Agent 作業，從 `Server1` 上的 SQL Server 2008 執行個體，移至 `Server2`上的 SQL Server 2016 執行個體。  `Jennie’s Report` 使用 `Sales` 資料庫。  `Sales` 目前不在目的地伺服器 `Server2`上。  `Server1` 將會在移動資料庫之後，重新指派給不同的小組。
  
6.  如先前的 [限制事項](#Restrictions)中所述，傳送參考尚不存在於目的地伺服器之資料庫的 SQL Server Agent 作業時，必須在目的地伺服器上建立 Shell 資料庫。  請在目的地伺服器上，建立名為 `Sales` 的 Shell 資料庫。 

7.  回到**精靈**的 [選取傳送方法] 頁面︰檢閱並保留預設值。  按一下 **[下一步]**。
  
8.  [選取資料庫] 頁面︰針對所需的資料庫 `Sales` 選取 [移動] 核取方塊。  按一下 **[下一步]**。
  
9.  [設定目的地資料庫] 頁面︰此**精靈**指出 `Sales` 已存在於目的地伺服器上 (如上述**步驟 6** 所建立)，並已在**目的地資料庫**名稱中附加 `_new`。  請從 [目的地資料庫] 文字方塊中刪除 `_new`。  如有需要，請變更 [檔案名稱] 和 [目的地資料夾]。  選取 [卸除目的地伺服器上具有相同名稱的資料庫，然後繼續資料庫傳送，並覆寫現有的資料庫檔案]。  按一下 **[下一步]**。
  
10. [選取伺服器物件] 頁面︰在 [選取的相關物件:] 面板中，按一下[Object name Logins (物件名稱登入)] 的省略符號按鈕。  在 [複製選項] 下，選取 [只複製選取的登入:]。  核取 [顯示所有伺服器登入] 的方塊。  核取 `contoso\Jennie` 的 [登入] 方塊。  按一下 **[確定]**。  在 [可用的相關的物件:] 面板中，選取 [SQL Server Agent 作業] 然後按一下 [>] 按鈕。  在 [選取的相關物件:] 面板中，按一下 [SQL Server Agent 作業] 的省略符號按鈕。  在 [複製選項] 下，選取 [只複製選取的作業]。  核取 [`Jennie’s Report`] 的方塊。  按一下 **[確定]**。  按一下 **[下一步]**。  
  
11. [來源資料庫檔案的位置] 頁面︰按一下 [來源伺服器上的檔案共用] 的省略符號按鈕，然後巡覽至指定的資料夾位置。  例如，針對資料夾位置 `D:\MSSQL13.MSSQLSERVER\MSSQL\DATA`，使用 `\\Server1\D$\MSSQL13.MSSQLSERVER\MSSQL\DATA` 作為 [來源伺服器上的檔案共用]。  按一下 **[下一步]**。
  
12. [設定封裝] 頁面︰在 [封裝名稱:] 文字方塊中，輸入 `SalesFromServer1toServer2_Move`。  核取 [是否要儲存傳送記錄檔?] 方塊。  在 [記錄選項] 下拉式清單中選取 [文字檔]。  記下 [錯誤記錄檔路徑]；請視需要進行修改。  按一下 **[下一步]**。  
  
     > **注意：**[錯誤記錄檔路徑] 是目的地伺服器上的路徑。
  
13. [排程封裝] 頁面︰從 [Integration Services Proxy 帳戶] 下拉式清單中選取相關的 Proxy。  按一下 **[下一步]**。

14. [完成精靈] 頁面︰檢閱所選選項的摘要。  按 **[上一步]** 即可變更選項。  按一下 [完成] 執行工作。  在傳送期間，[正在執行作業] 頁面會監視有關此**精靈**執行的狀態資訊。

15. [正在執行作業] 頁面︰如果作業成功，請按一下 [關閉]。  如果作業失敗，請檢閱錯誤記錄檔，也可選取 [上一步] 以進一步檢閱。  否則，請按一下 [關閉]。
  
16. **移動後步驟** ：考慮在新的主機 `Server2`上執行下列 T-SQL 陳述式：
  
     ~~~ tsql 
     ALTER AUTHORIZATION ON DATABASE::Sales TO sa;

     ALTER DATABASE Sales 
     SET COMPATIBILITY_LEVEL = 130;

     USE Sales
     GO

     EXEC sp_updatestats;
     ~~~
 
17. **移動後步驟清除**  
由於 `Server1` 會移至不同的小組，而且不會重複 **移動** 作業，因此請考慮執行下列步驟：
     -    刪除 `SalesFromServer1toServer2_Move` 上的 SSIS 封裝 `Server2`。
     -    刪除 `SalesFromServer1toServer2_Move` 上的 SQL Server Agent 作業 `Server2`。
     -    刪除 `Jennie’s Report` 上的 SQL Server Agent 作業 `Server1`。
     -    卸除 `contoso\Jennie` 上的登入 `Server1`。


### <a name="b-----copy-database-using-detach-and-attach-method-to-the-same-instance-and-set-recurring-schedule"></a>**B.   使用卸離與附加方法，將資料庫複製到相同的執行個體，並設定週期性排程。**  
在此範例中， `Sales` 資料庫會複製並建立為相同執行個體上的 `SalesCopy` 。  之後，`SalesCopy` 會每週重新建立一次。

6.  [選取傳送方法] 頁面︰檢閱並保留預設值。  按一下 **[下一步]**。

7.  [選取資料庫] 頁面︰針對 `Sales` 資料庫選取 [複製] 核取方塊。  按一下 **[下一步]**。

8.  [設定目的地資料庫] 頁面︰將**目的地資料庫**名稱變更為 `SalesCopy`。  如有需要，請變更 [檔案名稱] 和 [目的地資料夾]。  選取 [卸除目的地伺服器上具有相同名稱的資料庫，然後繼續資料庫傳送，並覆寫現有的資料庫檔案]。  按一下 **[下一步]**。

9.  [設定封裝] 頁面︰在 [封裝名稱:] 文字方塊中，輸入 `SalesCopy Weekly Refresh`。  核取 [是否要儲存傳送記錄檔?] 方塊。  按一下 **[下一步]**。

10. [排程封裝] 頁面︰按一下 [排程:] 選項按鈕，然後按一下 [變更排程] 按鈕。 
 
    1. [新增作業排程] 頁面︰在 [名稱] 文字方塊中，輸入 `Weekly on Sunday`。 
          
    2. 按一下 **[確定]**。

11. 從 [Integration Services Proxy 帳戶] 下拉式清單中選取相關的 Proxy。  按一下 **[下一步]**。

12. [完成精靈] 頁面︰檢閱所選選項的摘要。  按 **[上一步]** 即可變更選項。  按一下 [完成] 執行工作。  在封裝建立期間，[正在執行作業] 頁面會監視有關此**精靈**執行的狀態資訊。

13. [正在執行作業] 頁面︰如果作業成功，請按一下 [關閉]。  如果作業失敗，請檢閱錯誤記錄檔，也可選取 [上一步] 以進一步檢閱。  否則，請按一下 [關閉]。

14. 手動啟動新建立的 SQL Server Agent 作業 `SalesCopy weekly refresh`。  檢閱作業記錄，並確保執行個體上現在有 `SalesCopy` 。

  
##  <a name="FollowUp"></a> 待處理：升級資料庫之後  
 在您使用複製資料庫精靈，將資料庫從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，資料庫就會變成立即可用並自動進行升級。 如果資料庫具有全文檢索索引，升級程序就會根據 **[全文檢索目錄升級選項]** 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為 **[匯入]** 或 **[重建]**，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 **[匯入]**時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 如需有關檢視或變更 **全文檢索目錄升級選項** 屬性設定的詳細資訊，請參閱＜ [Manage and Monitor Full-Text Search for a Server Instance](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)＞。  
  
 如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。 如果已升級資料庫中的相容性層級為 90，則相容性層級會設定為 100 (這是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所支援的最低相容性層級)。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
 
 ## <a name="Post"></a> 複製或移動後的考量
 請考慮是否要在 **複製** 或 **移動**後執行下列步驟：
-    使用卸離與附加方法時，變更資料庫的擁有權。
-    **移動**後，卸除來源伺服器上的伺服器物件。
-    卸除此精靈在目的地伺服器上建立的 SSIS 封裝。
-    卸除此精靈在目的地伺服器上建立的 SQL Server Agent 作業。

  
## <a name="more-information"></a>詳細資訊！ 
 [使用卸離與附加來升級資料庫 &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [建立 SQL Server Agent Proxy](http://msdn.microsoft.com/library/142e0c55-a8b9-4669-be49-b9dc602d5988)  
  
  

