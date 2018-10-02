---
title: 建立連結的伺服器 (SQL Server Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords:
- linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c8caee5d7de5b348d6673636ac5cfc4704c3c51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625516"
---
# <a name="create-linked-servers-sql-server-database-engine"></a>建立連結的伺服器 (SQL Server Database Engine)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > 如需舊版 SQL Server 的相關內容，請參閱[建立連結的伺服器 (SQL Server 資料庫引擎)](create-linked-servers-sql-server-database-engine.md)。

  此主題說明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，建立連結的伺服器以及存取來自其他 [!INCLUDE[tsql](../../includes/tsql-md.md)]的資料。 透過建立連結的伺服器，您可以處理多個來源的資料。 連結的伺服器不必是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的另一個執行個體，但那是常見狀況。  
  
##  <a name="Background"></a> 背景  
 連結的伺服器可讓您對 OLE DB 資料來源存取分散式異質性查詢。 建立連結的伺服器之後，即可對這部伺服器執行分散式查詢，而且查詢可以加入來自多個資料來源的資料表。 如果連結的伺服器定義為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體，就可以執行遠端預存程序。  
  
 連結之伺服器的功能以及所需的引數可能會大大地改變。 本主題中的範例會提供一般範例，但不會描述所有選項。 如需詳細資訊，請參閱 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)的資料。  
  
##  <a name="Security"></a> 安全性  
  
### <a name="permissions"></a>[權限]  
 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，需要伺服器的 **ALTER ANY LINKED SERVER** 權限或 **setupadmin** 固定伺服器角色的成員資格。 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 時，需要 **CONTROL SERVER** 權限或 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
##  <a name="Procedures"></a> 如何建立連結的伺服器  
 您可以使用下列任一項：  
  
-   [Transact-SQL](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>若要使用 SQL Server Management Studio 建立與另一個 SQL Server 執行個體的連結伺服器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟 [物件總管]，展開 **[伺服器物件]**，以滑鼠右鍵按一下 **[連結的伺服器]**，然後按一下 **[新增連結的伺服器]**。  
  
2.  在 **[一般]** 頁面的 **[連結的伺服器]** 方塊中，輸入您要連結之 **[SQL Server]** 的執行個體名稱。  
  
     **[SQL Server]**  
     將連結的伺服器識別為 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 如果您使用這個定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連結之伺服器的方法， **[連結的伺服器]** 中所指定的名稱就必須是伺服器的網路名稱。 另外，從伺服器擷取的任何資料表，都會是來自已連結伺服器上之登入所定義的預設資料庫。  
  
     **其他資料來源**  
     指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外的 OLE DB 伺服器。 按一下這個選項會啟動在它下面的選項。  
  
     **提供者**  
     從清單方塊中選取 OLE DB 資料來源。 在登錄中，OLE DB 提供者是使用給定的 PROGID 註冊。  
  
     **產品名稱**  
     輸入 OLE DB 資料來源的產品名稱，以加入成為連結的伺服器。  
  
     **資料來源**  
     輸入資料來源的名稱，如 OLE DB 提供者所解譯。 如果您要連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體，請提供執行個體名稱。  
  
     **提供者字串**  
     輸入對應至資料來源之 OLE DB 提供者的唯一程式設計識別碼 (PROGID)。 如需有效提供者字串的範例，請參閱 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)的資料。  
  
     **位置**  
     依 OLE DB 提供者的解譯，輸入資料庫的位置。  
  
     **目錄**  
     輸入連接到 OLE DB 提供者時，要使用的目錄名稱。  
  
     若要測試連接到連結伺服器的能力，在 [物件總管] 中，以滑鼠右鍵按一下連結伺服器，然後按一下 **[測試連接]**。  
  
    > [!NOTE]  
    >  如果 **[SQL Server]** 的執行個體是預設的執行個體，請輸入裝載 **[SQL Server]** 執行個體之電腦的名稱。 如果 **SQL Server** 是具名執行個體，請輸入電腦的名稱和執行個體的名稱，例如 **Accounting\SQLExpress**。  
  
3.  在 **[伺服器類型]** 區域中，選取 **[SQL Server]** 表示連結的伺服器是 **[SQL Server]** 的另一個執行個體。  
  
4.  在 **[安全性]** 頁面上，指定原始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連線到連結的伺服器時將使用的安全性內容。 在使用者使用其網域登入進行連線的網域環境中，選取 **[使用登入的目前安全性內容建立]** 通常是最佳選擇。 當使用者使用 **[SQL Server]** 登入連線到原始 **[SQL Server]** 時，最佳選擇通常是選取 **[使用此安全性內容]**，然後提供所需的認證在連結的伺服器進行驗證。  
  
     **本機登入**  
     指定可以連接到連結伺服器的本機登入。 本機登入可以是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入或 Windows 驗證登入。 使用這份清單可限制與特定登入的連接，或允許某些登入連接成不同的登入。  
  
     **Impersonate**  
     將使用者名稱和密碼從本機登入傳送給連結伺服器。 若為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，則遠端伺服器上必須要有名稱和密碼完全相同的登入。 若為 Windows 登入，則登入必須是連結伺服器上的有效登入。  
  
     若要使用模擬，則組態必須符合委派需求。  
  
     **遠端使用者**  
     使用遠端使用者以對應未定義於 **[本機登入]** 中的使用者。 **[遠端使用者]** 必須是遠端伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入。  
  
     **遠端密碼**  
     指定遠端使用者的密碼。  
  
     **[加入]**  
     加入新的本機登入。  
  
     **移除**  
     移除現有的本機登入。  
  
     **不建立**  
     指定不會為未定義於清單中的登入建立連接。  
  
     **不使用安全性內容建立**  
     指定不會使用安全性內容為未定義於清單中的登入建立連接。  
  
     **使用登入的目前安全性內容建立**  
     指定使用登入的目前安全性內容為未定義於清單中的登入建立連接。 如果使用 Windows 驗證連接到本機伺服器，則會使用您的 Windows 認證來連接到遠端伺服器。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到本機伺服器，則會使用登入名稱和密碼來連接到遠端伺服器。 在此情況下，遠端伺服器上必須要有名稱和密碼完全相同的登入。  
  
     **使用此安全性內容建立**  
     指定使用 **[遠端登入]** 和 **[指定密碼]** 方塊中所指定的登入和密碼為未定義於清單中的登入建立連接。 遠端登入必須是遠端伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入。  
  
5.  (選擇性) 若要檢視或指定伺服器選項，請按一下 **[伺服器選項]**  頁面。  
  
     **定序相容**  
     影響針對連結伺服器的分散式查詢執行。 如果這個選項設為 true，關於字元集和定序順序 (或排序順序)， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會假設連結伺服器中的所有字元都與本機伺服器相容。 這會使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠將字元資料行的比較傳給提供者。 如果未設定這個選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一律會在本機環境中評估字元資料行的比較。  
  
     只有在確定對應於連結伺服器的資料來源與本機伺服器的字元集和排序順序相同時，才應該設定這個選項。  
  
     **資料存取**  
     啟用和停用連結伺服器的分散式查詢存取。  
  
     **RPC**  
     從指定伺服器啟用 RPC。  
  
     **RPC 輸出**  
     啟用對指定伺服器的 RPC。  
  
     **使用遠端定序**  
     決定將使用遠端資料行或本機伺服器的定序。  
  
     如果為 True，針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源會使用遠端資料行的定序，而針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源會使用定序名稱中所指定的定序。  
  
     如果為 False，分散式查詢一律會使用本機伺服器的預設定序，而定序名稱與遠端資料行的定序則會被忽略。 預設值為 False。  
  
     **定序名稱**  
     如果使用遠端定序為 True，並且資料來源不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源，請指定遠端資料來源所使用的定序名稱。 這個名稱必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所支援的定序之一。  
  
     當存取不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但其定序卻符合某項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序的 OLE DB 資料來源時，請使用這個選項。  
  
     連結伺服器必須支援供這部伺服器的所有資料行使用的單一定序。 如果連結伺服器支援單一資料來源內的多重定序，或無法確定連結伺服器的定序是否符合某項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序時，請勿設定這個選項。  
  
     **連接逾時**  
     連接到連結伺服器的逾時值 (以秒為單位)。  
  
     若為 0，則使用 **sp_configure** 的預設 [remote query timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) 選項值。  
  
     **查詢逾時**  
     針對連結伺服器進行查詢的逾時值 (以秒為單位)。  
  
     如果為 0，則使用 **sp_configure** 預設 [remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) 選項值。  
  
     **啟用分散式交易的升級**  
     使用此選項，透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 交易，保護伺服器對伺服器程序的動作。 此選項為 TRUE 時，呼叫遠端預存程序就會啟動分散式交易，而且會利用 MS DTC 來編列這項交易。 如需詳細資訊，請參閱 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)的資料。  
  
6.  按一下 **[確定]**。  
  
##### <a name="to-view-the-provider-options"></a>若要檢視提供者選項  
  
-   若要檢視提供者提供的選項，請按一下 **[提供者選項]** 頁面。  
  
     所有提供者的可用選項並不相同。 例如，某些資料類型有索引可用，而某些可能沒有。 使用這個對話方塊來幫助 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 了解提供者的功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會安裝某些共用的資料提供者，不過當提供資料的產品變更時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所安裝的該提供者不一定支援所有的最新功能。 提供資料之產品功能的最佳資源來源是該產品的說明文件。  
  
     **動態參數**  
     表示提供者允許在參數化查詢時使用 '?' 參數標記語法。 這個選項只有在提供者支援 **IcommandWithParameters** 介面，並支援 '?' 作為參數標記時才能設定。 設定這個選項允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 針對提供者執行參數化查詢。 針對提供者執行參數化查詢的能力，對於某些查詢而言可以達到較佳的效能。  
  
     **巢狀查詢**  
     表示該提供者允許 FROM 子句中使用巢狀 `SELECT` 陳述式。 設定這個選項允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向需要在 FROM 子句中包含巢狀 SELECT 陳述式的提供者委派某些查詢。  
  
     **限層級零**  
     只會針對提供者叫用層級 0 的 OLE DB 介面。  
  
     **允許 Inprocess**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許提供者被具現化為同處理序伺服器。 未設定此選項時，預設的行為便是將提供者具現化於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序之外。 將提供者起始於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序之外可以保護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序不會受到提供者發生錯誤的影響。 當提供者具現化於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序之外時，便不允許對要參考的長資料行 (**text**、 **ntext**或 **image**) 進行更新或插入。  
  
     **非交易更新**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 即使 **ITransactionLocal** 無法使用，仍然允許更新。 如果已啟用此選項，則針對提供者的更新便無法復原，因為提供者不支援交易。  
  
     **索引為存取路徑**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嘗試使用提供者的索引來提取資料。 依預設值，索引只用於中繼資料，絕不會開啟  
  
     **不允許特定存取**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許透過 OPENROWSET 與 OPENDATASOURCE 函數對 OLE DB 提供者進行特定存取。 未設定此選項時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也不會允許特定存取。  
  
     **支援 'Like' 運算子**  
     表示該提供者支援使用 LIKE 關鍵字的查詢。  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 若要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建立連結的伺服器，請使用 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)[CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md) 和 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md) 陳述式。  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>若要使用 Transact-SQL 建立與另一個 SQL Server 執行個體的連結伺服器  
  
1.  在查詢編輯器中，輸入下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令來連結名稱為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 `SRVR002\ACCTG`執行個體：  
  
    ```sql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  執行下列程式碼來設定連結的伺服器使用將使用連結的伺服器之登入的網域認證。  
  
    ```sql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a> 待處理：建立連結的伺服器之後所採取的步驟  
  
#### <a name="to-test-the-linked-server"></a>若要測試連結的伺服器  
  
-   執行下列程式碼來測試連結之伺服器的連線。 此範例會傳回連結之伺服器上的資料庫名稱。  
  
    ```sql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>撰寫加入來自連結伺服器之資料表的查詢  
  
-   使用四部分的名稱來表示連結之伺服器上的物件。 執行下列程式碼以傳回本機伺服器上的所有登入清單，及其連結之伺服器上相符的登入。  
  
    ```sql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     當連結的伺服器登入傳回 NULL 時，表示該登入不存在連結的伺服器上。 除非將連結的伺服器設定為傳遞不同的安全性內容，或連結的伺服器接受匿名連線，否則這些登入將無法使用連結的伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
