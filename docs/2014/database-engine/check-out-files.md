---
title: 簽出檔案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- Visual Studio.SourceControl.CheckOutDialog
helpviewer_keywords:
- checking out files
ms.assetid: cc033727-51bb-4b58-a12b-8977ce61ff56
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bde4d7fa738bdc952abc936ea13caa7225887ad6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786743"
---
# <a name="check-out-files"></a>簽出檔案
  除非您將 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 環境設成允許編輯簽入的檔案，否則，您必須先將檔案簽出，才能修改它。 當您簽出檔案時，會將檔案版本的副本複製到您的本機磁碟中，且必須移除檔案的唯讀屬性。  
  
 您可以採獨佔或共用的模式來簽出檔案。 當您以獨佔方式來簽出檔案時，在您重新簽入這個檔案之前，任何使用者都無法將它簽出。 當您以共用模式來簽出檔案時，其他使用者也可以簽出和修改這個檔案，則當您將它簽入時，可能需要合併您簽出的版本及其他使用者所建立的版本。  
  
 使用**簽出**命令來簽出原始檔控制專案和檔案。 如果您使用此命令來簽出方案或專案時，方案或專案中的所有檔案也將被都簽出。不過，簽出個別來源程式碼檔案不會導致簽出專案或其所屬的方案。  
  
> [!NOTE]  
>  如果[!INCLUDE[msCoName](../includes/msconame-md.md)]專案的 Visual SourceSafe 資料庫設定為允許多重簽出，而且您想要簽出檔案，您必須清除**允許多重簽出**選項**進階簽出選項**之前先簽出檔案 對話方塊。 您必須重新啟動 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，這項設定才會生效。  
  
### <a name="to-check-out-a-file"></a>簽出檔案  
  
1.  在 [方案總管] 中，選取專案或檔案。  
  
2.  在上**檔案**功能表上，指向**原始檔控制**，然後按一下**簽出以編輯**。  
  
3.  如果**簽出以編輯**對話方塊隨即出現，請選取的項目，然後按一下**簽出**。如果您已設定[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]環境，不想再顯示**簽出**對話方塊中，選取在 [方案總管] 和它們可能會有任何子系的項目都會立即簽出。  
  
     **請參閱**  
     簽出所有已選取的項目。  
  
     **資料行**  
     識別要顯示的資料行以及它們顯示的順序。  
  
     **註解**  
     指定要與簽出作業產生關聯的註解。  
  
     **簽出項目時，不要顯示簽出對話方塊**  
     簽出作業期間抑制此對話方塊。  
  
     **一般檢視**  
     在原始檔控制連接之下，以一般清單顯示正在簽出的項目。  
  
     **編輯**  
     修改未簽出的項目。**編輯** 按鈕隨即出現，只有當您擁有[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]設定為支援編輯簽入的檔案。  
  
     **名稱**  
     會顯示可簽出之項目的名稱。 選取的項目旁邊會顯示核取方塊。 如果您不要簽出特定項目，請清除其核取方塊。  
  
     **選項。**  
     按一下按鈕右邊的箭頭之後，就會顯示原始檔控制外掛程式特定的簽出選項。  
  
     **Sort**  
     排序顯示之資料行的順序。  
  
     **樹狀檢視**  
     顯示正在簽出之項目的資料夾與檔案階層。  
  
## <a name="see-also"></a>另請參閱  
 [編輯簽入的檔案](../../2014/database-engine/edit-checked-in-files.md)   
 [自動簽出時編輯的檔案](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [恢復簽出](../../2014/database-engine/undo-checkouts.md)   
 [管理簽出](../../2014/database-engine/manage-checkouts.md)  
  
  
