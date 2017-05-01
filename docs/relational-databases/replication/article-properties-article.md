---
title: "發行項屬性 - &lt;發行項&gt; | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.articleproperties.f1
helpviewer_keywords:
- Article Properties dialog box
ms.assetid: 6dd601a4-1233-43d9-a9f0-bc8d84e5d188
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d485cf7aface5f33fd4bd30f8c4a3d36707b2d2
ms.lasthandoff: 04/11/2017

---
# <a name="article-properties---ltarticlegt"></a>發行項屬性 - &lt;發行項&gt;
  從新增發行集精靈和 **[發行集屬性]** 對話方塊中，可以使用 **[發行項屬性]** 對話方塊。 它可讓您檢視和設定所有類型之發行項的屬性。 某些屬性只有在建立發行集時才能設定，而其他的則只有在發行集沒有使用中的訂閱時才能設定。 無法設定的屬性會以唯讀顯示。  
  
> [!NOTE]  
>  建立發行集之後，某些屬性變更需要新的快照集。 如果發行集有訂閱，則某些變更還需要重新初始化所有訂閱。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
 **[發行項屬性]** 對話方塊中的每個屬性均包含一個描述。 按一下某個屬性，在對話方塊底部會顯示其描述。 此主題提供數個屬性的其他資訊。 屬性會依下列類別目錄分組：  
  
-   套用至所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的屬性。  
  
-   從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]套用至交易式發行集的屬性。  
  
-   套用至合併式發行集的屬性。  
  
-   從 Oracle 發行者套用至交易式和快照式發行集的屬性。  
  
## <a name="options-for-all-publications"></a>所有發行集的選項  
 **[複製資料表資料分割結構描述]** 和 **[複製索引資料分割結構描述]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入資料表資料分割和索引資料分割，這與透過資料列和資料行篩選提供的資料分割複寫不相關。 **[複製資料表資料分割結構描述]** 和 **[複製索引資料分割結構描述]** 選項，會指定是否應將資料分割結構描述複製到訂閱者。 如需有關資料分割的詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)＞。  
  
 **轉換資料類型**  
 在訂閱者端建立物件時，決定是否從使用者自訂資料類型轉換為基底資料型別。 使用者定義資料類型包括 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中導入的使用者定義 CLR 類型。 如果您要將這些資料類型複寫到舊版的 **，請指定** [True] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值；這可確保訂閱者端能夠正確地處理這些類型。  
  
 **在訂閱者端建立結構描述**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入了結構描述，這是使用 CREATE SCHEMA 陳述式來定義的。 結構描述是物件的擁有者 (在多重部分名稱中使用)，例如 \<資料庫>.\<結構描述>.\<物件>。 如果您有物件位於 DBO 以外之結構描述所擁有的資料庫中，複寫就可以在訂閱者端建立這些結構描述，使得發行的物件得以建立。  
  
 如果您要將資料複寫到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]版本：  
  
-   請將此選項設定為 **[False]**，因為舊版並不支援 CREATE SCHEMA。  
  
-   針對每個結構描述，請使用和結構描述相同的名稱，將使用者加入至訂閱資料庫。  
  
 **[將 XML 轉換為 NTEXT]**、 **[將 MAX 資料類型轉換為 NTEXT 和 IMAGE]**、 **[將新的日期時間轉換為 NVARCHAR]**、 **[將檔案資料流轉換為 MAX 資料類型]**、 **[將大的 CLR 轉換為 MAX 資料類型]**、 **[將 hierarchyId 轉換為 MAX 資料類型]**和 **[將空間轉換為 MAX 資料類型]**。  
 決定是否要依照描述的方式轉換資料類型和屬性。 如果您要將這些資料類型複寫至舊版 **，請指定** [True] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值。 這樣做可確保系統會在訂閱者端正確處理它們。  
  
 **目的地物件名稱**  
 在訂閱資料庫中建立之物件的名稱。 無法為針對點對點異動複寫啟用之發行集內的發行項變更此選項。  
  
 **目的地物件擁有者**  
 在訂閱資料庫中建立之物件的結構描述。 預設是發行集資料庫中物件所屬的結構描述，例外狀況如下：  
  
-   針對相容性層級小於 90 之合併式發行集內的發行項：依預設，會將擁有者保留空白，並在訂閱者上建立物件期間，將其指定為 **dbo** 。  
  
-   針對 Oracle 發行集內的發行項：依預設，會將擁有者指定為 **dbo**。  
  
-   針對使用字元模式快照集之發行集內的發行項 (用於非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者和 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者)：依預設，會將擁有者保留空白。 擁有者預設為與散發代理程式或合併代理程式用於連接到訂閱者之帳戶相關聯的擁有者。  
  
 無法為針對點對點異動複寫啟用之發行集內的發行項變更此選項。  
  
 **自動管理識別範圍**  
 依預設，複寫會管理發行者端和每個訂閱者的所有識別欄位。 每個複寫節點都會被指派一個範圍的識別值 (使用 **[發行者範圍大小]** 和 **[訂閱者範圍大小]** 選項來指定)，以確保給定值只用於一個節點。 如需詳細資訊，請參閱[複寫識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
## <a name="options-for-transactional-publications"></a>交易式發行集的選項  
 **複製 INSERT、UPDATE 和 DELETE 預存程序**  
 在此對話方塊的 **[陳述式傳遞]** 區段中，如果您選取使用預存程序將變更傳播到訂閱者 (預設值)，請選取是否也要將這些程序複製到每個訂閱者。 如果您選取 **[False]**，則必須手動複製程序，否則散發代理程式在嘗試傳遞變更時將會失敗。  
  
 **Statement delivery**  
 本節中的選項適用於所有資料表，包括當做資料表複寫的索引檢視表。 除非您的應用程式需要不同的功能，否則[!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用預設選項。 依預設，異動複寫會透過每個訂閱者上所安裝的一組預存程序，將變更傳播到訂閱者。 在發行者端的資料表上進行插入、更新或刪除時，作業會翻譯為對訂閱者端預存程序的呼叫。  
  
 **[傳遞陳述式]** 選項會指定是否使用預存程序，如果是，傳遞至程序的參數應使用何種格式。 **[預存程序]** 選項可以讓您使用複寫自動建立的程序，或者替代您建立的自訂程序。  
  
 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
 **複寫**  
 此選項僅適用於儲存程序。 它決定是否要複寫預存程序 (CREATE PROCEDURE 陳述式) 或其執行的定義。 如果您複寫程序的執行，程序定義會在初始化訂閱之後複寫到訂閱者端；在發行者端執行程序時，複寫會在訂閱者端執行對應的程序。 這可在執行大量批次作業時大幅提升效能。 如需詳細資訊，請參閱＜ [Publishing Stored Procedure Execution in Transactional Replication](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)＞。  
  
## <a name="options-for-merge-publications"></a>合併式發行集的選項  
 合併式發行集的 **[發行項屬性]** 對話方塊有兩個索引標籤： **[屬性]** 和 **[解析程式]**。  
  
### <a name="properties-tab"></a>屬性索引標籤  
 **同步處理方向**  
 決定是否可從使用下列客訂閱類型的訂閱者上傳變更：  
  
-   **[雙向]** (預設值)：可以將變更下載至訂閱者，和上傳至發行者。  
  
-   **[僅限下載至訂閱者，禁止訂閱者變更]**：可以將變更下載至訂閱者，但無法上傳至發行者。 觸發程序防止在訂閱者端進行變更。  
  
-   **[僅限下載至訂閱者，允許訂閱者變更]**：可以將變更下載至訂閱者，但無法上傳至發行者。  
  
 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **資料分割選項**  
 指定參數化篩選所建立之資料分割的類型。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞的「設定資料分割選項」一節。  
  
 **追蹤層級**  
 決定是否將相同資料列或相同資料行的變更視為衝突。  
  
 **[確認 INSERT 權限]**、 **[確認 UPDATE 權限]**和 **[確認 DELETE 權限]**  
 在同步處理期間，決定是否檢查訂閱者登入在發行集資料庫之已發行的資料表上有 INSERT、UPDATE 或 DELETE 權限。 預設值為 **[False]** ，因為合併式複寫並不需要取得這些權限；存取已發行的資料表是透過發行集存取清單 (PAL) 控制。 如需 PAL 的詳細資訊，請參閱[保護發行者](../../relational-databases/replication/security/secure-the-publisher.md)。  
  
 如果您要允許一或多個訂閱者上傳某些變更到已發行的資料，而非其他的資料時，您可以要求檢查權限。 例如，您可以將訂閱者加入至 PAL，但是不在發行集資料庫的資料表上給予訂閱者任何權限。 接著，您可以將 [確認 DELETE 權限] 設定為 **[True]**：訂閱者能夠上傳插入和更新，但無法上傳刪除。  
  
 **多重資料行 UPDATE**  
 當合併式複寫執行更新時，它會更新一個 UPDATE 陳述式中所有已變更的資料行，並將未變更的資料行重設為其原始值。 這些案例的替代方法是發出多個 UPDATE 陳述式，針對每個已變更的資料行使用一個 UPDATE 陳述式。 多重資料行 UPDATE 陳述式通常較有效率，但如果資料表上的觸發程序設定為回應特定資料行的更新，且因發生更新時的資料行重設造成回應不正確，則應考慮將此選項設定為 **[False]** 。  
  
> [!IMPORTANT]  
>  此選項已被取代，並將在未來的版本中移除。  
  
### <a name="resolver-tab"></a>解析程式索引標籤  
 **使用預設解析程式**  
 如果您選取預設的解析程式，則會依據指派給每個訂閱者的優先權或第一個寫入發行者的變更來解決衝突，視使用的訂閱類型而定。 如需詳細資訊，請參閱[偵測及解決合併式複寫衝突](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)。  
  
 **使用自訂解析程式 (已在散發者註冊)**  
 如果您選擇使用發行項解析程式 (由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 提供或您自行撰寫)，您必須從清單方塊中選取解析程式。 如需詳細資訊，請參閱＜ [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)＞。  
  
 如果解析程式需要任何輸入，請在 **[輸入解析程式所需的資訊]** 文字方塊中進行指定。 如需有關 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 自訂解析程式所需之輸入的詳細資訊，請參閱＜ [Microsoft COM-Based Resolvers](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)＞。  
  
 **允許訂閱者在視需要同步期間，以互動方式解決衝突**  
 如果訂閱者會使用視需要同步 (合併式複寫的預設值)，而且您要以互動方式解決衝突，則選取此選項。 在新增訂閱精靈的 **[同步排程]** 頁面上指定視需要同步。 若要以互動方式解決衝突，請使用互動解析程式使用者介面。 如需詳細資訊，請參閱＜ [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)＞。  
  
 **要求在合併前先驗證數位簽章**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 提供的所有以 COM 為基礎的解析程式都已簽署。 選取此選項即可驗證同步處理時解析程式是有效的。  
  
## <a name="options-for-oracle-publications"></a>Oracle 發行集的選項  
 Oracle 發行集的 **[發行項屬性]** 對話方塊有兩個索引標籤： **[屬性]** 和 **[資料對應]**。 Oracle 發行集並不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集支援的所有屬性。 如需詳細資訊，請參閱＜ [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)＞。  
  
### <a name="properties-tab"></a>屬性索引標籤  
 **複製 INSERT、UPDATE 和 DELETE 預存程序**  
 在此對話方塊的 **[陳述式傳遞]** 區段中，如果發行項在交易式發行集內，且您選取使用預存程序將變更傳播到訂閱者 (預設值)，請選取是否也要將這些程序複製到每個訂閱者。 如果您選取 **[False]**，則必須手動複製程序，否則散發代理程式在嘗試傳遞變更時將會失敗。  
  
 **目的地物件擁有者**  
 如果您輸入 **[dbo]**以外的值：  
  
-   針對執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本的訂閱者，您必須確定在訂閱者端使用和輸入之值相同的名稱來建立結構描述。 如需詳細資訊，請參閱 [CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)。  
  
-   針對執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]之前版本的訂閱者，請針對每個結構描述，使用和結構描述相同的名稱將使用者加入到訂閱資料庫。  
  
 **資料表空間名稱**  
 建立複寫的資料表空間會變更 Oracle 伺服器執行個體上的追蹤資料表。 如需詳細資訊，請參閱[管理 Oracle 資料表空間](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)。  
  
 **Statement delivery**  
 本節中的選項適用於交易式發行集中的所有資料表。 除非您的應用程式需要不同的功能，否則[!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用預設選項。 依預設，異動複寫會透過每個訂閱者上所安裝的一組預存程序，將變更傳播到訂閱者。 在發行者端的資料表上進行插入、更新或刪除時，作業會翻譯為對訂閱者端預存程序的呼叫。  
  
 **[傳遞陳述式]** 選項會指定是否使用預存程序，如果是，傳遞至程序的參數應使用何種格式。 **[預存程序]** 選項可以讓您使用複寫自動建立的程序，或者替代您建立的自訂程序。  
  
 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
### <a name="data-mapping-tab"></a>資料對應索引標籤  
 **資料行名稱**  
 發行者端之資料行的名稱 (唯讀)。  
  
 **發行者資料類型**  
 發行者端之資料行的 Oracle 資料類型 (唯讀)。 此資料類型只可以直接在 Oracle 資料庫中進行變更。 如需詳細資訊，請參閱 Oracle 文件集。  
  
 **訂閱者資料類型**  
 複寫資料時，Oracle 資料類型對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型：  
  
-   針對某些資料類型，只有一個可能的對應，在此情況下，屬性方格中的資料行為唯讀。  
  
-   對於某些資料類型，有多種類型可供您選擇。 除非您的應用程式需要不同的對應，否則[!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用預設對應。 如需詳細資訊，請參閱＜ [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視和修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
