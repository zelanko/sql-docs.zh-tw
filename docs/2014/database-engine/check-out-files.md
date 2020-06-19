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
ms.openlocfilehash: 10c076f7bee35e0e466fc22aec9ad9f6984bac6a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936029"
---
# <a name="check-out-files"></a>簽出檔案
  除非您將 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 環境設成允許編輯簽入的檔案，否則，您必須先將檔案簽出，才能修改它。 當您簽出檔案時，會將檔案版本的副本複製到您的本機磁碟中，且必須移除檔案的唯讀屬性。  
  
 您可以採獨佔或共用的模式來簽出檔案。 當您以獨佔方式來簽出檔案時，在您重新簽入這個檔案之前，任何使用者都無法將它簽出。 當您以共用模式來簽出檔案時，其他使用者也可以簽出和修改這個檔案，則當您將它簽入時，可能需要合併您簽出的版本及其他使用者所建立的版本。  
  
 使用 [**簽出**] 命令來簽出原始檔控制的專案和檔案。 如果您使用這個命令來簽出方案或專案，則也會簽出方案或專案中的所有檔案。不過，簽出個別的原始程式碼檔案並不會導致簽出它所屬的專案或方案。  
  
> [!NOTE]  
>  如果 [!INCLUDE[msCoName](../includes/msconame-md.md)] 您專案的 Visual SourceSafe 資料庫設定為允許多個簽出，而您想要以獨佔方式簽出檔案，您必須在簽出檔案之前，清除 [**高級簽出選項**] 對話方塊中的 [**允許多次簽**出] 選項。 您必須重新啟動 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，這項設定才會生效。  
  
### <a name="to-check-out-a-file"></a>簽出檔案  
  
1.  在 [方案總管] 中，選取專案或檔案。  
  
2.  **在 [檔案**] 功能表上，指向 [原始檔**控制**]，然後按一下 [**簽出] 進行編輯**。  
  
3.  如果顯示 [**簽出進行編輯**] 對話方塊，請選取您想要的專案，然後按一下 [**簽出**]。如果您已將 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境設定為不顯示 [**簽出**] 對話方塊，則會立即簽出方案總管中選取的專案，以及他們可能擁有的任何子系。  
  
     **退房**  
     簽出所有已選取的項目。  
  
     **資料行**  
     識別要顯示的資料行以及它們顯示的順序。  
  
     **註解**  
     指定要與簽出作業產生關聯的註解。  
  
     **簽出項目時不要顯示簽出對話方塊**  
     簽出作業期間抑制此對話方塊。  
  
     **一般檢視**  
     在原始檔控制連接之下，以一般清單顯示正在簽出的項目。  
  
     **編輯**  
     修改專案但不簽出。只有**Edit**在您已 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 設定為支援編輯簽入檔案時，才會出現 [編輯] 按鈕。  
  
     **名稱**  
     會顯示可簽出之項目的名稱。 選取的項目旁邊會顯示核取方塊。 如果您不要簽出特定項目，請清除其核取方塊。  
  
     **選項**  
     按一下按鈕右邊的箭頭之後，就會顯示原始檔控制外掛程式特定的簽出選項。  
  
     **方式**  
     排序顯示之資料行的順序。  
  
     **樹狀檢視**  
     顯示正在簽出之項目的資料夾與檔案階層。  
  
## <a name="see-also"></a>另請參閱  
 [編輯簽入的檔案](../../2014/database-engine/edit-checked-in-files.md)   
 [在編輯時自動簽出檔案](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [復原簽出](../../2014/database-engine/undo-checkouts.md)   
 [管理簽出](../../2014/database-engine/manage-checkouts.md)  
  
  
