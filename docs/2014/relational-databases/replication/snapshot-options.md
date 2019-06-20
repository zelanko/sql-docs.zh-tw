---
title: 修改 SQL 複寫的快照集初始化選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 2a611de458537156740521dae8b732eed3e2653c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270247"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>修改 SQL 複寫的快照集初始化選項

這篇文章討論如何修改一些選項的時機[使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)。

## <a name="snapshot-format"></a>快照集格式
  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上，指定快照集格式。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)＞。  

1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上，選取 [原生 SQL Server - 所有訂閱者都必須是執行 SQL Server 的伺服器]  或 [字元 - 如果發行者或訂閱者沒有執行 SQL Server 則需要]  。 

    > [!NOTE]  
    >  建議選取原生格式，除非此發行集必須支援對 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 資料庫或非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的訂閱。    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="snapshot-folder-locations"></a>快照集資料夾位置

### <a name="default-snapshot-location"></a>預設快照集位置
指定預設快照集位置 (SQL Server Management Studio) 指定預設快照集的位置**快照集資料夾**的 「 設定散發精靈 」 的頁面。 如需使用此精靈的詳細資訊，請參閱[設定發行和散發](configure-publishing-and-distribution.md)。 如果您在未設定為「散發者」的伺服器上建立發行集，則請在「新增發行集精靈」的 **[快照集資料夾]** 頁面中指定預設快照集位置。 如需使用此精靈的詳細資訊，請參閱[建立發行集](publish/create-a-publication.md)。  
  
 在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，修改預設快照集位置。 如需詳細資訊，請參閱[檢視及修改散發者和發行者屬性](view-and-modify-distributor-and-publisher-properties.md)。 在 [發行集屬性 - \<發行集>]  對話方塊中為每個發行集設定快照集資料夾。 如需詳細資訊，請參閱 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  
  
#### <a name="modify-the-default-snapshot-location"></a>修改預設快照集位置  
  
1.  在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，按一下您要變更其預設快照集位置之發行者的屬性按鈕 ( **...** )。    
2.  在 [發行者屬性 - \<發行者>]  對話方塊中，輸入 [預設快照集資料夾]  屬性的值。

    > [!NOTE]  
    >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](security/secure-the-snapshot-folder.md)。    
1.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

### <a name="alternate-snapshot-location"></a>替代快照集位置
  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面中指定替代快照集位置。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)＞。 

  
#### <a name="specify-an-alternate-snapshot-location"></a>指定替代快照集位置  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上：    
    1.  選取 **[將檔案放在下列資料夾中]** ，然後按一下 **[瀏覽]** 以瀏覽至目錄，或者輸入應儲存快照集檔案之目錄的路徑。    

        > [!NOTE]  
        >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](security/secure-the-snapshot-folder.md)。    
    a.  除非您需要將快照集檔案寫入兩個位置，否則請清除 **[將檔案放在預設資料夾]** 。    
     若要壓縮快照集檔案，請選取 **[壓縮這個位置中的快照集檔案]** 。 壓縮通常用於低頻寬連接和抽取式媒體上的替代快照集位置，例如 CD-ROM。    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]   


## <a name="compress-snapshot-files"></a>壓縮快照集檔案
在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上，指定要壓縮檔案。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)＞。  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上：  
  
    1.  選取 **[將檔案放在下列資料夾中]** ，然後按一下 **[瀏覽]** 以瀏覽至目錄，或者輸入應儲存快照集檔案之目錄的路徑。    
        > [!NOTE]  
        >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 若是使用提取訂閱，則必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](security/secure-the-snapshot-folder.md)。  
  
    2.  除非您需要將快照集檔案寫入兩個位置，否則請清除 **[將檔案放在預設資料夾]** 。    
        > [!NOTE]  
        >  如果選取這個核取方塊，則不會壓縮儲存在預設資料夾中的檔案。 壓縮的檔案只能儲存在上一個步驟中指定的其他位置。    
2.  選取 **[壓縮此資料夾中的快照集檔案]** 。    
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>在套用快照集之前及之後執行指令碼

 您可以指定在套用快照集之前或之後在「訂閱者」端執行指令碼。 指令碼在很多情況下都會用到，例如在各「訂閱者」端建立登入和結構描述 (物件擁有者) 時。  
  
 為各指令碼指定檔案位置後，每次進行快照集處理時，「快照集代理程式」便會將指令碼檔案複製到目前的快照集資料夾中。 套用快照集時，「散發代理程式」或「合併代理程式」會在執行任何複寫物件指令碼之前，先執行前快照集指令碼。 並在套用所有其他複寫物件指令碼及資料之後，執行後快照集指令碼。 快照集應用程式完成且指令碼檔案成功執行之後，會從「訂閱者」的工作目錄中移除指令碼檔案。  
  
 啟動 **sqlcmd** 公用程式即可執行指令碼。 部署指令碼之前，請使用 **sqlcmd** 執行指令碼，以確保能按預期執行。 在套用快照集前後執行的指令碼內容必須能夠重複。 例如，如果在指令碼中建立資料表，應先檢查該資料表是否已存在，如果存在，再採取適當動作。 指令碼必須能夠重複，因為當您需要重新初始化已套用了指令碼的訂閱時，該指令碼便會在新快照集於重新初始化期間套用時重新被套用。  
  
 若要壓縮快照集檔案 (將其儲存為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 檔案格式)，指令碼也會壓縮並儲存到 CAB 檔案中。 將壓縮的快照集檔傳送給「訂閱者」並解壓縮至「訂閱者」的工作目錄後，將執行任何指示為前快照集指令碼的指令碼。 同樣地，在套用快照集的最後一個步驟中，也會在「訂閱者」端解壓縮並執行後快照集指令碼。  

### <a name="execute-a-script-before-or-after-a-snapshot-is-applied"></a>在套用快照集前後執行指令碼  
 在 [發行集屬性 - \<發行集>]  對話方塊之 [快照集]  頁面上套用快照集的前後，指定要執行的選擇性指令碼。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)＞。  


1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [快照集]  頁面上：    
    -   若要在套用快照集之前指定要執行的指令碼，請按一下 **[瀏覽]** 以瀏覽到指令碼，或在 **[套用快照前執行此指令碼]** 文字方塊中輸入指令碼的路徑。 
   
        > [!NOTE]  
        >  「散發代理程式」或「合併代理程式」必須具有指定目錄的讀取權限。 如果使用提取訂閱，則必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\電腦名稱\scripts\myscript.sql。    
    -   若要在套用快照集之後指定要執行的指令碼，請按一下 **[瀏覽]** 以瀏覽到指令碼，或在 **[套用快照後執行此指令碼]** 文字方塊中輸入指令碼的路徑。    
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
