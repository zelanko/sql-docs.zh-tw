---
title: "設定 Oracle 發行者 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
caps.latest.revision: 60
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2eb98196756e47a5118c8cf777a6ef5e05b950f4
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="configure-an-oracle-publisher"></a>設定 Oracle 發行者
  「Oracle 發行者」之發行集的建立方式與典型的快照式及交易式發行集的建立方式相同，但是在從「Oracle 發行者」端建立發行集之前，您必須完成下列步驟 (步驟一、三和四在本主題中有詳細描述)：  
  
1.  使用提供的指令碼在 Oracle 資料庫中建立複寫管理使用者。  
  
2.  對於您將發行的資料表，則在每個資料表上直接 (不透過角色) 將 SELECT 權限授與您在步驟一中建立的 Oracle 管理使用者。  
  
3.  在「 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上安裝 Oracle 用戶端軟體和 OLE DB 提供者，然後停止並重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。 如果「散發者」在 64 位元平台上執行，則必須使用 Oracle OLE DB 提供者的 64 位元版本。  
  
4.  在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端將 Oracle 資料庫設為「發行者」。  
  
 如需可以從 Oracle 資料庫複寫的物件清單，請參閱 [Oracle 發行者的設計考量與限制](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)。  
  
> [!NOTE]  
>  您必須是 **sysadmin** 固定伺服器角色的成員，才能啟用「發行者」或「散發者」並建立 Oracle 發行集或從 Oracle 發行集建立訂閱。  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>在 Oracle 資料庫中建立複寫管理的使用者結構描述  
 複寫代理程式連接到 Oracle 資料庫並在您必須建立的使用者結構描述內容中執行作業。 此結構描述必須被授與許多權限，這些權限會列示在下一節中。 此結構描述在「Oracle 發行者」上擁有 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫處理所建立的所有物件，但公用同義字 **MSSQLSERVERDISTRIBUTOR**除外。 如需 Oracle 資料庫中建立的物件的詳細資訊，請參閱＜ [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)＞。  
  
> [!NOTE]  
>  用 **CASCADE** 選項來卸除 **MSSQLSERVERDISTRIBUTOR** 公用同義字和設定的 Oracle 複寫使用者，會從「Oracle 發行者」移除所有的複寫物件。  
  
 在 Oracle 複寫使用者結構描述的安裝程式中會提供範例指令碼進行輔助。 安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 後，可在下列目錄中取得此指令碼：*\<磁碟機>*:\\\Program Files\Microsoft SQL Server\\*\<執行個體名稱>*\MSSQL\Install\oracleadmin.sql。 它也包含在＜ [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)＞主題中。  
  
 使用具有 DBA 權限的帳戶連接到 Oracle 資料庫並執行指令碼。 此指令碼會提示輸入複寫管理使用者結構描述的使用者與密碼，以及要在其中建立物件的預設資料表空間 (資料表空間必須已經存在於 Oracle 資料庫中)。 如需如何為物件指定其他資料表空間的資訊，請參閱[管理 Oracle 資料表空間](../../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)。 可以選擇任何使用者名稱和增強式密碼，但是需將兩者都記下來，因為稍後當您將 Oracle 資料庫設為「發行者」時會提示需要此資訊。 建議僅將結構描僅用於複寫所需的物件；不要建立資料表來發行於此結構描述中。  
  
### <a name="creating-the-user-schema-manually"></a>手動建立使用者結構描述  
 如果您手動建立複寫管理使用者結構描述，則必須授與結構描述下列權限 (不論是直接或透過資料庫角色)。  
  
-   CREATE PUBLIC SYNONYM 和 DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 您還必須直接 (不透過角色) 授與使用者下列權限：  
  
-   CREATE ANY TRIGGER。 只有快照集和異動複寫中才需要這個權限。  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>在 SQL Server 散發者上安裝和設定 Oracle 用戶端網路軟體  
 您必須在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上安裝並設定 Oracle 用戶端網路軟體和 Oracle OLE DB 提供者，如此「散發者」才能連接到「Oracle 發行者」。 安裝該軟體後，請在安裝該軟體的資料夾上設定適當的權限，然後停止並重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，確定所有的設定都已更新 (權限會在＜設定目錄權限＞一節中描述)。  
  
> [!NOTE]  
>  Oracle 用戶端網路軟體必須是最新的可用版本。 Oracle 建議使用者安裝最新版本的用戶端軟體。 因此用戶端軟體的版本通常比資料庫軟體的版本還要新。  
  
 安裝和設定用戶端網路軟體最直接的方法是使用 Oracle Client 磁碟上的 Oracle Universal Installer 和 Net Configuration Assistant。  
  
 在 Oracle Universal Installer 中，您將提供下列資訊：  
  
|資訊|描述|  
|-----------------|-----------------|  
|Oracle Home|這是到 Oracle 軟體之安裝目錄的路徑。 接受預設路徑 (C:\oracle\ora90 或類似路徑) 或輸入其他路徑。 如需有關 Oracle Home 的詳細資訊，請參閱本主題後面的「Oracle Home 的注意事項」。|  
|Oracle Home 名稱|Oracle Home 路徑的別名。|  
|安裝類型|在 Oracle 10g 中，選取 **[管理員]** 安裝選項。|  
  
 Oracle Universal Installer 完成之後，請使用 Net Configuration Assistant 設定網路連接性。 您必須提供四項資訊來設定網路連接性。 Oracle 資料庫管理員會在設定資料庫與接聽程式時設定網路組態，如果您沒有此一資訊，管理員應該能夠提供。 您必須執行下列工作：  
  
|動作|描述|  
|------------|-----------------|  
|識別資料庫|有兩種方法可以識別資料庫。 第一種方法使用 Oracle 系統識別碼 (SID)，每個 Oracle 版本都有。 第二種方法使用服務名稱，從 Oracle 8.0 版開始提供。 這兩種方法都使用在建立資料庫時設定的值，重要的是，用戶端網路組態必須使用相同於管理員在設定資料庫接聽程式時，所使用的命名方法。|  
|識別資料庫的網路別名|您必須指定一個用於存取 Oracle 資料庫的網路別名。 在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端將 Oracle 資料庫視為「發行者」時也要提供此別名。 網路別名實質上是指向在建立資料庫時設定之遠端 SID 或服務名稱的指標；不同的 Oracle 版本與產品中所使用的稱呼各有不同，包括網路服務名稱 (Net Service Name) 和 TNS 別名 (TNS Alias)。 您登入時，SQL*Plus 會提示以「Host String」參數輸入這個別名。|  
|選取網路通訊協定|選取您要支援的適當通訊協定。 大多數應用程式使用 TCP。|  
|指定識別資料庫接聽程式的主機資訊|主機是 Oracle 接聽程式所執行之電腦 (通常與資料庫所在的電腦相同) 的名稱或 DNS 別名。 針對某些通訊協定，您必須提供其他的資訊。 例如，您若是選取 TCP，就必須提供接聽程式接聽對目標資料庫之連接要求的通訊埠。 預設 TCP 組態使用通訊埠 1521。|  
  
### <a name="setting-directory-permissions"></a>設定目錄權限  
 必須授與「散發者」端執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務時所用的帳戶，對安裝 Oracle 用戶端網路軟體之目錄 (及所有子目錄) 的讀取和執行權限。  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>測試 SQL Server 散發者和 Oracle 發行者之間的連接  
 在 Net Configuration Assistant 執行即將結束時，可能會出現一個用於測試到「Oracle 發行者」連接的選項。 在您測試連接之前，請確定 Oracle 資料庫執行個體有上線，而且 Oracle 接聽程式正在執行。 如果測試不成功，請連絡負責您想要連接之資料庫的 Oracle DBA (Oracle 資料庫管理員)。  
  
 如果成功連接到「Oracle 發行者」，則嘗試使用與您建立之複寫管理使用者結構描述相關聯的帳戶和密碼登入資料庫。 當以 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務使用的 Windows 帳戶執行時，必須執行下列項目：  
  
1.  按一下 **[開始]**，然後按一下 **[執行]**。  
  
2.  輸入 `cmd` ，然後按一下 **[確定]**。  
  
3.  在命令提示字元中，輸入：  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     例如： `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  如果網路組態成功，登入將會成功，您也會看到 `SQL` 提示字元。  
  
5.  如果您遇到連接到 Oracle 資料庫的問題，請參閱在＜ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ＞中的「 [ssNoVersion](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)＞。  
  
### <a name="considerations-for-oracle-home"></a>Oracle Home 的注意事項  
 Oracle 支援應用程式二進位編碼檔案的並存安裝，但是複寫時，一次只能使用一組二進位編碼檔案。 每一個二進位編碼檔案與一個 Oracle Home 相關聯；二進位編碼檔案是在 %ORACLE_HOME%\bin 目錄下。 如果複寫連接到「Oracle 發行者」，則您必須確定使用正確的二進位編碼檔案集 (特別對於最新版本的用戶端網路軟體)。  
  
 利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務使用的帳戶登入散發者，並設定適當的環境變數。 %ORACLE_HOME% 變數應設定為參考您安裝用戶端網路軟體時指定的安裝點。 %PATH% 必須包含 %ORACLE_HOME% \bin 目錄，做為遇到的第一個 Oracle 項目。 如需有關設定環境變數的資訊，請參閱 Windows 文件集。  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>在 SQL Server 散發者端將 Oracle 資料庫設為發行者  
 「Oracle 發行者」通常使用遠端「散發者」；您必須設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體充當「Oracle 發行者」的「散發者」 (「Oracle 發行者」只能使用一個「散發者」，但是單一「散發者」可以服務多個「 Oracle 發行者」)。 設定「散發者」之後，透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 、Transact-SQL 或 Replication Management Objects (RMO) 將 Oracle 資料庫執行個體視為「 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]散發者」端的「發行者」。 如需設定「散發者」的詳細資訊，請參閱 [設定散發](../../../relational-databases/replication/configure-distribution.md)。  
  
> [!NOTE]  
>  Oracle 發行者的名稱不能與其 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者相同，也不能與使用同一散發者的任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者相同。  
  
 將 Oracle 資料庫視為「發行者」時，您必須選擇 Oracle 發行選項：[完整] 或 [Oracle 閘道]。 識別發行者之後，除非卸除並重新設定發行者，否則無法變更此選項。 [完整] 選項設計用於為 Oracle 發行提供具備全部支援功能的快照式和交易式發行集。 [Oracle 閘道] 選項在複寫充當系統間閘道的情況下提供特定的設計最佳化以增進效能。  
  
 在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端識別「Oracle 發行者」後，複寫會建立名稱與 Oracle 資料庫之 TNS 服務名稱相同的連結伺服器。 此連結伺服器只能由複寫使用。 若您必須透過連結伺服器連線來連接到 Oracle 發行者，請建立另一個 TNS 服務名稱，然後在呼叫 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 時使用這個名稱。  
  
 若要設定 Oracle 發行者並建立發行集，請參閱＜ [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [Oracle 發行者的管理考量](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Oracle 發行者的資料類型對應](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Oracle 發行相關術語字彙](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
