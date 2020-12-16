---
title: 發行集屬性 - 對話方塊
description: 描述 SQL Server Management Studio (SSMS) 內 [發行集屬性] 對話方塊中顯示的頁面。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.filterrows.f1
- sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1
- sql13.rep.newpubwizard.pubproperties.general.f1
- sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1
- sql13.rep.newpubwizard.pubproperties.snapshotformat.f1
helpviewer_keywords:
- Publication Properties dialog box
ms.assetid: 66e845e9-1308-4288-9110-ad2f22f1fc58
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: fa48c38c00732759cf49c8fb694a54f8bc210971
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483019"
---
# <a name="sql-server-replication-publication-properties--dialog-box"></a>SQL Server 複寫 [發行集屬性] 對話方塊
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

本頁說明 [發行集屬性] 對話方塊內的頁面。 

## <a name="general"></a>一般
 **[發行集屬性]** 對話方塊的 **[一般]** 頁面，包含發行集的基本資訊，例如名稱、描述和訂閱到期原則。  
  
### <a name="options"></a>選項。  
 **名稱**  
 發行集的名稱 (唯讀)。  
  
 **Database**  
 發行集資料庫的名稱 (唯讀)。  
  
 **說明**  
 發行集的描述。  
  
 **型別**  
 發行集的類型 (唯讀)。  
  
 **訂閱過期**  
 選取其中一個訂閱過期選項：[訂閱永遠不會過期] 或 [訂閱會過期]，並提供明確的時間週期 (**間隔**)。  
  
 針對快照式發行集和交易式發行集， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您接受預設的 **[訂閱永遠不會過期]** 設定。  
  
 針對合併式複寫， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您接受預設的 **[訂閱會過期]** 設定，並將 **[間隔]** 儘可能設成較低的值。 隨著訂閱過期週期長度的增加，儲存的中繼資料量也會跟著增加，因而可能影響效能。 請在中斷訂閱者的連接或長時間不進行同步處理，以及儲存和處理大量中繼資料可能造成的效能問題之間，進行評估以取得平衡點。  
  
 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 **相容性層級**  
 僅限 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本，而且僅限合併式發行集。 選取與此發行集同步處理之訂閱者所需的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最低版本。 決定相容性層級的相關規則有數個。  

## <a name="filter-rows"></a>篩選資料列
  **[發行集屬性]** 對話方塊的 **[篩選資料列]** 頁面，可以讓您進行加入、編輯或刪除：  
  
-   將靜態資料列篩選套用至快照集式、交易式和合併式發行集的資料表發行項。   
-   將參數化資料列篩選器套用至合併式發行集的資料表發行項。    
-   使用聯結篩選，將合併資料表發行項的篩選擴充到相關的資料表發行項。 如需篩選選項的詳細資訊，請參閱[篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)。  
  
> [!NOTE]  
>  需要有發行集的新快照集，而且要重新初始化所有訂閱，才能加入、編輯或刪除篩選。  
  
若要使應用程式效能最佳化，並減少需要的遠端儲存體數量，或限制特定訂閱者對特定資料的存取，您就應該只發行需要的資料。 發行集可同時包括未篩選和已篩選的資料表。 例如，您可以包括公司產品的完整 (未篩選) 資料表，並使用資料列篩選來提供已篩選過、僅包含特定區域之客戶的資料表。 利用篩選發行的資料，您可以：  
  
-   將透過網路傳送的資料總量縮減到最少。    
-   降低訂閱者端所需的儲存空間量。    
-   依照個別的訂閱者需求，自訂發行集和應用程式。    
-   可以避免或減少訂閱者更新資料時的衝突，因為不同資料分割可以傳送給不同的訂閱者 (不會有兩個訂閱者同時更新相同的資料值)。    
-   避免傳送機密資料。 資料列篩選與資料行篩選可用於限制訂閱者對資料的存取。 對於合併式複寫，如果使用含有 HOST_NAME() 的參數化篩選，則有安全性考量。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「使用 HOST_NAME() 進行篩選」一節。  
  
### <a name="options"></a>選項。  
 **已篩選的資料表**  
 當您在發行集的資料表發行項中加入篩選時，這些篩選就會擴展到窗格中。 含有資料列篩選的資料表，會顯示為窗格中的最上層節點。 若為合併式發行集，則透過聯結篩選而擴充篩選的資料表，就會顯示為子節點。  
  
 **加入**  
 按一下 **[加入]** 即可啟動一個可讓您篩選資料表發行項的對話方塊。 在快照集或交易式發行集按一下 **[加入]** 會立即啟動對話方塊。 針對合併式發行集按一下 [加入] 會顯示三個選項：[加入篩選]、[加入聯結以擴充選取的篩選]，以及 [自動產生篩選]。  
  
-   選取 **[加入篩選]** 即可啟動 **[加入篩選]** 對話方塊。 這個對話方塊可以讓您套用資料列篩選至資料表發行項。 例如，在 **[加入篩選]** 對話方塊中，您可以指定含有客戶資料的資料表在複寫到訂閱者時，只能包含法國客戶的資料。  
  
-   選取 **[加入聯結以擴充選取的篩選]** 即可啟動 **[加入聯結]** 對話方塊。 **[加入聯結]** 對話方塊可以讓您擴充資料列篩選，使它篩選與具有資料列篩選的資料表相關之資料表中的資料。 例如，如果客戶資料表經過篩選後只包含法國客戶的資料，而它有一個包含客戶訂單的相關資料表，那麼您就可以在兩個資料表之間定義聯結，使訂單資料表只包括法國客戶的訂單。  
  
    > [!NOTE]  
    >  唯有當您先在篩選窗格中選取聯結的基底資料表，才能使用此選項。  
  
-   選取 **[自動產生篩選]** 來啟動 **[產生篩選]** 對話方塊。 這個對話方塊可讓您在合併式發行集的一個資料表上定義資料列篩選，複寫時會自動將此篩選擴充到因外部索引鍵關聯性而相關的其他資料表。 例如，發行集可包括 3 個資料表：客戶資料表、訂單資料表 (含有客戶資料表的外部索引鍵) 和訂單明細資料表 (含有訂單資料表的外部索引鍵)。 在客戶資料表上定義資料列篩選，複寫時會將它擴充到其他資料表。  
  
    > [!NOTE]  
    >  當複寫自動產生篩選時，發行集上任何現有的篩選都會被刪除。 若要同時包括自動產生的篩選和手動指定的篩選，請先產生篩選。 您只能對每個發行集指定一個自動產生的篩選集。  
  
 **編輯**  
 在篩選窗格中選取資料列篩選或聯結篩選，再按一下 **[編輯]** ，即可啟動 **[編輯篩選]** 或 **[編輯聯結]** 對話方塊。  
  
 **刪除**  
 在篩選窗格中選取資料列篩選或聯結篩選，再按一下 **[刪除]** 即可刪除篩選。  
  
 **尋找資料表**  
 僅合併式發行集。 按一下 **[尋找資料表]** ，即可在複雜篩選樹中尋找資料表。 在含有複雜關聯性的資料庫中，因為資料表可以聯結到多個資料表，所以資料表可能重複出現在篩選樹的多個位置。  
  
 實際資料表只出現在篩選樹的一個位置，而在其他位置，資料表是以捷徑方式顯示。 資料表的捷徑只是資料表的參考，它不會顯示資料表的子節點。 捷徑節點會以捷徑箭號標示，展開該節點會顯示這段文字：**按一下 [尋找資料表]，以查看 \<tablename> 的資料表**。  
  
 在窗格中選取捷徑節點，然後按一下 **[尋找資料表]** ，窗格就會展開並反白該資料表。 如果您按一下 **[尋找資料表]** 但未選取捷徑節點，則會啟動 **[尋找資料表]** 對話方塊。  
  
 **Filter**  
 包含在篩選窗格中選取之篩選的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定義。  

## <a name="publication-access-list"></a>發行集存取清單
  **[發行集屬性]** 對話方塊的 **[發行集存取清單]** 頁面，可以讓您從發行集存取清單 (PAL) 加入與移除登入、帳戶和群組。 PAL 是保護發行者安全的主要機制。 建立發行集之後，複寫便會建立此發行集的 PAL。 PAL 的功能與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 存取控制清單相似，其中包含被授與存取發行集的登入、帳戶和群組之清單。  
  
 當訂閱者連接到發行者或散發者並要求存取發行集時，訂閱者的登入會與 PAL 的驗證資訊比較。 如此可以為發行者提供額外的安全性，因為這會防止用戶端工具利用發行者與散發者的登入直接在發行者上進行修改。 如需詳細資訊，請參閱[保護發行者](../../relational-databases/replication/security/secure-the-publisher.md)。  
  
### <a name="options"></a>選項。  
 **加入**  
 加入一個新項目到清單中。 您只能加入在發行者端和散發者端都已經定義的登入、帳戶或群組。 如果您使用網域帳戶或在兩個伺服器上都已經建立本機帳戶，則它們就已同時在兩個伺服器上定義完成。  
  
 **移除**  
 從清單中移除選取的項目。  
  
 **全部移除**  
 從清單中移除所有的項目。  

## <a name="ftp-snapshot-and-internet"></a>FTP 快照集和網際網路

-   設定屬性以經由檔案傳輸通訊協定 (File Transfer Protocol，FTP) 傳遞快照集。 如需詳細資訊，請參閱[透過 FTP 傳遞快照集](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)。 若要使用 FTP 傳遞快照集，您必須設定 FTP 伺服器。 請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文件集以取得詳細資訊。  
  
    > [!NOTE]  
    >  FTP 設定若有任何變更，就需要產生新的快照集。  
  
-   針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本上的合併式複寫，設定 Web 同步處理的屬性，即可讓訂閱透過 HTTPS (安全超文字傳輸通訊協定) 進行同步處理。 若要使用 Web 同步處理，您必須設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 伺服器。 如需詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。  
  
### <a name="options"></a>選項。  
 **透過 FTP 存取快照集檔案**  
 選取 **[允許訂閱者使用 FTP (檔案傳輸通訊協定) 下載快照集檔案]** ，並指定 **[FTP 伺服器名稱]** 、 **[通訊埠編號]** 、 **[FTP 根資料夾的路徑]** 、 **[登入]** 和 **[密碼]** ，即可讓訂閱者使用 FTP 傳遞快照集。  
  
 此選項可以讓訂閱者使用 FTP 擷取快照集檔案，但這並不是必要的。 如果您選取此選項，新增訂閱精靈就會預設讓訂閱者經由 FTP 擷取快照集檔案。 若要變更此設定，請使用 **[訂閱屬性]** 對話方塊。 如果您讓訂閱者經由 FTP 存取快照集檔案，請在 **[快照集屬性]** 對話方塊的 **[快照集]** 頁面上，指定 FTP 資料夾作為快照集檔案的位置。 這樣做會在新的快照集產生時，讓快照集代理程式自動更新 FTP 資料夾中的檔案。 如果位置沒有設定到 FTP 資料夾，當新的快照集產生時，您就必須手動更新檔案。 如需詳細資訊，請參閱[透過 FTP 傳遞快照集](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)。  
  
 **Web 同步處理**  
 僅限合併式複寫。 選取 **[允許訂閱者連接到 Web 伺服器進行同步處理]** ，並指定 Web 伺服器位址讓合併式訂閱者使用 Web 同步處理。 Web 伺服器必須使用傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL))，且網址必須完整，例如 `https://server.domain.com/synchronize`。 如需詳細資訊，請參閱 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  


## <a name="agent-security"></a>代理程式安全性
  **[發行集屬性]** 對話方塊的 **[代理程式安全性]** 頁面，可以讓您存取執行下列代理程式的帳戶設定，並與複寫拓撲中的電腦建立連接：  
  
-   所有發行集的快照集代理程式。  
  
-   所有交易式發行集的記錄讀取器代理程式。 每個為異動複寫發行的資料庫，都會有一個記錄讀取器代理程式。 變更記錄讀取器代理程式會影響資料庫中的所有交易式發行集。  
  
-   允許佇列更新訂閱之交易式發行集的佇列讀取器代理程式。 每個散發資料庫都會有一個佇列讀取器代理程式。 變更佇列讀取器代理程式的設定，會影響使用相同散發資料庫之具有佇列更新訂閱的交易式發行集。 如需「佇列讀取器代理程式」安全性設定的詳細資訊，請參閱[檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 如需有關每一個代理程式所需的安全性設定和權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
### <a name="options"></a>選項。  
 **[安全性設定]** 或 **[建立代理程式]**  
 如果已建立代理程式作業，請按一下 **[安全性設定]** 來存取對話方塊，即可讓您變更代理程式的安全性設定。 如果尚未建立代理程式作業，請按一下 **[建立代理程式]** ，即可建立代理程式並指定安全性設定。  

## <a name="data-partitions"></a>分割區
分割區  
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]  
  **[發行集屬性]** 對話方塊的 **[資料分割]** 頁面，可讓您定義使用參數化篩選之合併式發行集的資料分割。 定義資料分割之後，您可以為這些資料分割產生快照集，依據訂閱者的連接屬性 (登入及/或電腦名稱)，為不同的訂閱者提供不同的初始資料集。 如果訂閱者在第一次同步處理資料分割時沒有可用的快照集，您也可以選取來允許訂閱者要求快照集傳遞和產生。 如需詳細資訊，請參閱 [使用參數化篩選建立合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
### <a name="options"></a>選項。  
 **加入**  
 按一下 **[加入]** 即可定義資料分割。 在 **[加入資料分割]** 對話方塊中，指定 **HOST_NAME()** 及/或 **SUSER_SNAME()** 的值，並定義排程來重新整理快照集。  
  
 **編輯**  
 在方格中選取現有的資料分割，然後按一下 **[編輯]** 來編輯資料分割。  
  
 **刪除**  
 在方格中選取現有的資料分割，然後按一下 **[刪除]** 來刪除資料分割。  
  
 **立即產生選取的快照集**  
 在方格中選取一或多個資料分割，然後按一下 **[立即產生選取的快照集]** 來產生這些資料分割的快照集。  
  
 **清除現有快照集**  
 在方格中選取一或多個資料分割，然後按一下 **[清除現有快照集]** 來清除這些資料分割的快照集。  
  
 **新的訂閱者嘗試同步處理時，可以視需要自動定義資料分割並產生快照集。**  
 如果您要允許訂閱者要求快照集產生和應用程式，請選取此選項。 如果訂閱者在第一次同步處理資料分割時沒有可用的快照集，則可能需要此選項。  

## <a name="snapshot"></a>快照式
快照式  
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]  
  **[發行集屬性]** 對話方塊的 **[快照集]** 頁面，可以讓您設定快照集格式、快照集資料夾位置以及在快照集的應用程式之前和之後執行的指令碼。 快照集資料夾必須指定為共用，而且會讀取和寫入檔案到資料夾的代理程式需要有足夠的權限。 如需適當地保護資料夾的詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
> [!NOTE]  
>  發行集需要有新的快照集才能進行變更。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
### <a name="options"></a>選項。  
 **快照集格式**  
 為快照集格式選取原生模式或字元模式。  
  
-   如果所有的訂閱者都是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，而非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的執行個體，請選取 [原生 SQL Server - 所有訂閱者都必須是執行 SQL Server 的伺服器]。 原生快照集格式可以提供最佳的效能。    
-   如果有任何訂閱者正在執行 **，或為非** 訂閱者，請選取 [!INCLUDE[ssEW](../../includes/ssew-md.md)] [字元 - 如果發行者或訂閱者沒有執行 SQL Server 則需要][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。    
 **快照集檔案的位置**  
 選取儲存快照集檔案的位置。 這些檔案可以儲存在預設位置；也可以儲存在取代預設位置的替代位置，或除了預設位置以外的替代位置。 儲存在替代位置的檔案可以壓縮。  
  
-   選取 **[將檔案放在預設資料夾]** ，以使用發行者的預設快照集資料夾。 在此對話方塊中的快照集資料夾位置是唯讀的，因為只能在 **[散發者屬性]** 對話方塊中為發行者進行變更。 如需詳細資訊，請參閱[修改快照集屬性](../../relational-databases/replication/snapshot-options.md)。    
-   選取 **[將檔案放在下列資料夾中]** ，以指定取代預設位置的替代位置，或除了預設位置以外的替代位置。 在文字方塊中輸入路徑，或按一下 **[瀏覽]** 並瀏覽到適當位置。 選取 **[壓縮此資料夾中的快照集檔案]** ，以壓縮在替代快照集位置中的檔案。 替代位置可以位於其他伺服器、網路磁碟機或抽取式媒體 (例如 CD-ROM 或抽取式磁碟) 上。 如需詳細資訊，請參閱[修改快照集屬性](../../relational-databases/replication/snapshot-options.md)。  
  
 **執行其他指令碼**  
 指定在訂閱者端套用快照集之前和之後要執行的指令碼。 如果 **[快照集格式]** 是 **[字元]** ，則無法指定指令碼。  
  
 指令碼是選擇性的，但可提供便於執行命令以及在訂閱者端套用管理變更的方式。 如需執行指令碼的詳細資訊，請參閱[在套用快照集之前及之後執行指令碼](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。  
  
-   在 **[套用快照集之前執行此指令碼]** 文字方塊中輸入路徑，或按一下 **[瀏覽]** 以指定指令碼的位置。    
-   在 **[套用快照集之後執行此指令碼]** 文字方塊中輸入路徑，或按一下 **[瀏覽]** 以指定指令碼的位置。 
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   

  
  
