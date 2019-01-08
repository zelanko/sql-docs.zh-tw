---
title: 發行集屬性、快照集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.snapshotformat.f1
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7d94874d03c05fffbc62743b5337649a3e228a2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804400"
---
# <a name="publication-properties-snapshot"></a>發行集屬性，快照集
  **[發行集屬性]** 對話方塊的 **[快照集]** 頁面，可以讓您設定快照集格式、快照集資料夾位置以及在快照集的應用程式之前和之後執行的指令碼。 快照集資料夾必須指定為共用，而且會讀取和寫入檔案到資料夾的代理程式需要有足夠的權限。 如需適當地保護資料夾的詳細資訊，請參閱[保護快照集資料夾](security/secure-the-snapshot-folder.md)。  
  
> [!NOTE]  
>  發行集需要有新的快照集才能進行變更。 如需詳細資訊，請參閱[變更發行集與發行項屬性](publish/change-publication-and-article-properties.md)。  
  
## <a name="options"></a>選項。  
 **快照集格式**  
 為快照集格式選取原生模式或字元模式。  
  
-   如果所有的訂閱者都是  的執行個體，而非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，請選取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. 原生快照集格式可以提供最佳的效能。  
  
-   如果有任何訂閱者正在執行 **，或為非** 訂閱者，請選取 [!INCLUDE[ssEW](../../includes/ssew-md.md)] [字元 - 如果發行者或訂閱者沒有執行 SQL Server 則需要][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **快照集檔案的位置**  
 選取儲存快照集檔案的位置。 這些檔案可以儲存在預設位置；也可以儲存在取代預設位置的替代位置，或除了預設位置以外的替代位置。 儲存在替代位置的檔案可以壓縮。  
  
-   選取 **[將檔案放在預設資料夾]** ，以使用發行者的預設快照集資料夾。 在此對話方塊中的快照集資料夾位置是唯讀的，因為只能在 **[散發者屬性]** 對話方塊中為發行者進行變更。 如需詳細資訊，請參閱[指定預設快照集位置 &#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md)。  
  
-   選取 **[將檔案放在下列資料夾中]** ，以指定取代預設位置的替代位置，或除了預設位置以外的替代位置。 在文字方塊中輸入路徑，或按一下 **[瀏覽]** 並瀏覽到適當位置。 選取 **[壓縮此資料夾中的快照集檔案]** ，以壓縮在替代快照集位置中的檔案。 替代位置可以位於其他伺服器、網路磁碟機或抽取式媒體 (例如 CD-ROM 或抽取式磁碟) 上。 如需相關資訊，請參閱 [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md) 及 [Compressed Snapshots](compressed-snapshots.md)。  
  
 **執行其他指令碼**  
 指定在訂閱者端套用快照集之前和之後要執行的指令碼。 如果 **[快照集格式]** 是 **[字元]**，則無法指定指令碼。  
  
 指令碼是選擇性的，但可提供便於執行命令以及在訂閱者端套用管理變更的方式。 如需執行指令碼的詳細資訊，請參閱[在套用快照集之前及之後執行指令碼](execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   在 **[套用快照集之前執行此指令碼]** 文字方塊中輸入路徑，或按一下 **[瀏覽]** 以指定指令碼的位置。  
  
-   在 **[套用快照集之後執行此指令碼]** 文字方塊中輸入路徑，或按一下 **[瀏覽]** 以指定指令碼的位置。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](publish/create-a-publication.md)   
 [檢視及修改發行集屬性](publish/view-and-modify-publication-properties.md)   
 [建立和套用初始快照集](create-and-apply-the-initial-snapshot.md)   
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)   
 [發行資料和資料庫物件](publish/publish-data-and-database-objects.md)  
  
  
