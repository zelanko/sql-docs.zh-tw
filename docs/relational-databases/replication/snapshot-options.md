---
title: 修改 SQL 複寫的快照集初始化選項 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 526f97ab2427aa6834614c9b31201b780ae25e9e
ms.sourcegitcommit: 636c02bd04f091ece934e78640b2363d88cac28d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67860541"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>修改 SQL 複寫的快照集初始化選項 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[使用快照集來初始化訂閱](initialize-a-subscription-with-a-snapshot.md)時，有幾個要指定的選項。

## <a name="specify-snapshot-format-sql-server-management-studio"></a>指定快照集格式 (SQL Server Management Studio)
  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上，指定快照集格式。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
### <a name="to-specify-snapshot-format"></a>若要指定快照集格式  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上，選取 [原生 SQL Server - 所有訂閱者都必須是執行 SQL Server 的伺服器]  或 [字元 - 如果發行者或訂閱者沒有執行 SQL Server 則需要]  。  
  
    > [!NOTE]  
    >  建議您選取原生格式，除非此發行集必須支援對 SQL Server Compact 資料庫或非 SQL Server 資料庫的訂閱。  
  
2.  選取 [確定]  。   

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="snapshot-folder-locations"></a>快照集資料夾位置

### <a name="default-snapshot-location"></a>預設快照集位置
在「設定散發精靈」的 **[快照集資料夾]** 頁面中指定預設快照集位置。 如需使用此精靈的詳細資訊，請參閱[設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)。 如果您在未設定為「散發者」的伺服器上建立發行集，則請在「新增發行集精靈」的 **[快照集資料夾]** 頁面中指定預設快照集位置。 如需使用此精靈的詳細資訊，請參閱[建立發行集](../../relational-databases/replication/publish/create-a-publication.md)。  
  
 在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，修改預設快照集位置。 如需詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。 在 [發行集屬性 - \<發行集>]  對話方塊中為每個發行集設定快照集資料夾。 如需詳細資訊，請參閱 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### <a name="to-modify-the-default-snapshot-location"></a>若要修改預設快照集位置  
  
1.  在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，按一下您要變更其預設快照集位置之發行者的屬性按鈕 ( **...** )。    
2.  在 [發行者屬性 - \<發行者>]  對話方塊中，輸入 [預設快照集資料夾]  屬性的值。  
  
    > [!NOTE]  
    >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。    
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
 

### <a name="alternate-snapshot-locations"></a>替代的快照集位置
替代的快照集位置可以讓您將快照集檔案儲存到預設位置以外的地方，通常是位於「散發者」。 替代位置可以位於其他伺服器、網路磁碟機或抽取式媒體 (例如 CD-ROM 或抽取式磁碟)。  
  
替代的快照集位置會儲存為發行集的屬性。 因為替代快照集位置是一種發行集屬性，「散發代理程式」和「合併代理程式」可以尋找適當的快照集做為同步處理的一部份。  
  
如果您要指定替代快照集的資料夾位置或是壓縮快照集檔，請立即建立發行集 (但不要立刻建立初始快照集)、設定快照集位置的發行集屬性，然後對此發行集執行「快照集代理程式」(Snapshot Agent)。 如果您在建立初始快照集後變更替代位置，則不會將發行集任何產生的快照集重新放置到新的替代位置。 在此狀況下，「合併代理程序」或「散發代理程序」可能無法在新的替代位置找到快照集檔案，這取決於此發行集的設定。  
  
> [!NOTE]  
>  請勿使用 [發行集屬性]  對話方塊或 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 指定與預設快照集資料夾位置相同的替代位置。  
  
> [!CAUTION]  
>  請勿同時使用 WebSync 和替代快照集資料夾位置。  
  
#### <a name="use-sql-server-management-studio"></a>使用 SQL Server Management Studio
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上：  
  
    1.  選取 **[將檔案放在下列資料夾中]** ，然後按一下 **[瀏覽]** 以瀏覽至目錄，或者輸入應儲存快照集檔案之目錄的路徑。  
  
        > [!NOTE]  
        >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
    2.  除非您需要將快照集檔案寫入兩個位置，否則請清除 **[將檔案放在預設資料夾]** 。  
  
     若要壓縮快照集檔案，請選取 **[壓縮這個位置中的快照集檔案]** 。 壓縮通常用於低頻寬連接和抽取式媒體上的替代快照集位置，例如 CD-ROM。  
  
2.  選取 [確定]  。  
  
#### <a name="use-transact-sql"></a>使用 Transact-SQL 

[設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md) 時，請將 **snapshot_in_defaultfolder** 的值指定為 False。 

## <a name="compressed-snapshots"></a>壓縮的快照集
  當您透過通訊緩慢的網路傳送快照集時，或將快照集儲存到抽取式媒體中，且未壓縮的快照集過大而未能放入媒體時，適合壓縮快照集檔案。 在這種狀況下，壓縮快照集檔案非常有用，但是壓縮會增加產生及套用快照集的時間。  
  
 將壓縮的快照集檔案以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 檔案格式寫入，可以壓縮 2 GB 或更小的檔案 (如果快照集檔案大於 2 GB，則不能壓縮)。 若要壓縮檔案，必須將它們寫入替代的快照集資料夾 (不能壓縮寫入預設快照集資料夾的檔案)。 
  
 檔案在執行「散發代理程式」或「合併式代理程式」的位置解壓縮；發送訂閱通常與壓縮的快照集一起使用，以便檔案在「訂閱者」端解壓縮。 當「訂閱者」收到壓縮檔案時，檔案最初會寫入暫存位置。 壓縮的檔案複製到「訂閱者」之後，壓縮檔案中的快照集檔案會被解壓縮，CAB 公用程式會依順序一次解壓縮一個檔案。 「訂閱者」端需要的空間是壓縮檔案加上最大未壓縮檔案的大小。  
  
> [!NOTE]  
>  在某些情況下，壓縮的快照集可以改善網路之間傳送快照集檔案的效能。 不過，壓縮快照集需要由快照集代理程式在產生快照集檔案時，進行其他處理動作；並於套用快照集檔案時，進行散發代理程式或合併代理程式。 如此可能會減緩快照集的產生且在某些情況下會增加套用快照集的時間。 此外，若發生網路失敗，則無法繼續壓縮快照集；因此並不適合不穩定的網路。 透過網路使用壓縮快照集時，仔細考量這些權衡問題。  
  
### <a name="use-sql-server-management-studio"></a>使用 SQL Server Management Studio
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上：  
  
    1.  選取 **[將檔案放在下列資料夾中]** ，然後按一下 **[瀏覽]** 以瀏覽至目錄，或者輸入應儲存快照集檔案之目錄的路徑。  
  
        > [!NOTE]  
        >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 若是使用提取訂閱，則必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](security/secure-the-snapshot-folder.md)。  
  
    2.  除非您需要將快照集檔案寫入兩個位置，否則請清除 **[將檔案放在預設資料夾]** 。  
  
        > [!NOTE]  
        >  如果選取這個核取方塊，則不會壓縮儲存在預設資料夾中的檔案。 壓縮的檔案只能儲存在上一個步驟中指定的其他位置。  
  
2.  選取 **[壓縮此資料夾中的快照集檔案]** 。    
3.  選取 [確定]  。   

### <a name="use-transact-sql"></a>使用 Transact-SQL

[設定快照集屬性](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)時，請將 **compress_snapshot** 的值指定為 **True**。 

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>在套用快照集之前及之後執行指令碼
您可以指定在套用快照集之前或之後在「訂閱者」端執行指令碼。 指令碼在很多情況下都會用到，例如在各「訂閱者」端建立登入和結構描述 (物件擁有者) 時。  
  
 為各指令碼指定檔案位置後，每次進行快照集處理時，「快照集代理程式」便會將指令碼檔案複製到目前的快照集資料夾中。 套用快照集時，「散發代理程式」或「合併代理程式」會在執行任何複寫物件指令碼之前，先執行前快照集指令碼。 並在套用所有其他複寫物件指令碼及資料之後，執行後快照集指令碼。 快照集應用程式完成且指令碼檔案成功執行之後，會從「訂閱者」的工作目錄中移除指令碼檔案。  
  
 啟動 **sqlcmd** 公用程式即可執行指令碼。 部署指令碼之前，請使用 **sqlcmd** 執行指令碼，以確保能按預期執行。 在套用快照集前後執行的指令碼內容必須能夠重複。 例如，如果在指令碼中建立資料表，應先檢查該資料表是否已存在，如果存在，再採取適當動作。 指令碼必須能夠重複，因為當您需要重新初始化已套用了指令碼的訂閱時，該指令碼便會在新快照集於重新初始化期間套用時重新被套用。  
  
 若要壓縮快照集檔案 (將其儲存為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 檔案格式)，指令碼也會壓縮並儲存到 CAB 檔案中。 將壓縮的快照集檔傳送給「訂閱者」並解壓縮至「訂閱者」的工作目錄後，將執行任何指示為前快照集指令碼的指令碼。 同樣地，在套用快照集的最後一個步驟中，也會在「訂閱者」端解壓縮並執行後快照集指令碼。  

### <a name="execute-a-script"></a>執行指令碼 

1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上：    
    -   若要在套用快照集之前指定要執行的指令碼，請按一下 **[瀏覽]** 以瀏覽到指令碼，或在 **[套用快照前執行此指令碼]** 文字方塊中輸入指令碼的路徑。  
  
        > [!NOTE]  
        >  「散發代理程式」或「合併代理程式」必須具有指定目錄的讀取權限。 如果使用提取訂閱，則必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\電腦名稱\scripts\myscript.sql。  
  
    -   若要在套用快照集之後指定要執行的指令碼，請按一下 **[瀏覽]** 以瀏覽到指令碼，或在 **[套用快照後執行此指令碼]** 文字方塊中輸入指令碼的路徑。   
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  


## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [透過 FTP 傳送快照集](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)   
 [設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)     
  
  
