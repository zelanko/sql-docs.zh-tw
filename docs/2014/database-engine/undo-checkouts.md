---
title: 恢復簽出 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourcControl.UndoCheckDialog
helpviewer_keywords:
- checking out files
- checkout source controls [SQL Server]
- undoing checkouts
ms.assetid: a6596b20-3aa5-4dc4-a4c5-3649f1f5a20e
caps.latest.revision: 22
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 273f7c1ccb5a9e55864df27939ff39e7f04787d5
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811544"
---
# <a name="undo-checkouts"></a>復原簽出
  您可以使用**恢復簽出**命令來取消現有的簽出。 當您修改且儲存了某個檔案之後，又需要回復這些變更時，這尤其有用。  
  
 您設定的選項而定**復原簽出進階選項** 對話方塊中，Studio 環境在本機磁碟上保留的項目工作複本或取代的原始檔控制的最新版本。 如果有人在原始檔控制系統的環境之外修改了這個項目，擷取的版本便可能不是最新的版本。  
  
### <a name="to-undo-a-checkout"></a>恢復簽出  
  
1.  在 [方案總管] 中，選取一個專案。  
  
2.  在 **檔案**功能表上，指向**原始檔控制**，然後按一下**恢復簽出**。  
  
3.  在 **恢復簽出** 對話方塊中，選取適當的選項，然後按一下**恢復簽出** 按鈕。  
  
     **資料行**  
     識別要顯示的資料行以及它們顯示的順序。  
  
     **一般檢視**  
     在原始檔控制連接下，以一般清單的方式顯示項目。  
  
     **名稱**  
     顯示要恢復簽出的項目名稱。 項目出現時，旁邊的核取方塊會顯示為已選取。 如果您不想恢復項目的簽出，請清除該核取方塊。  
  
     **選項。**  
     按一下按鈕右邊的箭頭之後，就會顯示原始檔控制外掛程式特定的恢復簽出選項。  
  
     **排序**  
     排序顯示資料行的順序。  
  
     **樹狀檢視**  
     顯示您要反轉簽出之項目的資料夾和項目階層。  
  
     **復原簽出**  
     反轉簽出，捨棄對簽出檔案所做的任何變更。  
  
## <a name="see-also"></a>另請參閱  
 [簽出檔案](../../2014/database-engine/check-out-files.md)   
 [管理簽出](../../2014/database-engine/manage-checkouts.md)  
  
  
