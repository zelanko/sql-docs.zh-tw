---
title: 簽入檔案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckInDialog
helpviewer_keywords:
- checking in files
ms.assetid: 0657a387-8411-4406-bef9-d262a5bfa269
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5debb7c80e7365e67d8661709b09b16f5d25b7b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096768"
---
# <a name="check-in-files"></a>簽入檔案
  若要將您修改過的原始檔控制檔案提供給其他使用者，您必須將這些檔案簽入原始檔控制中。 當您簽入檔案時，您簽入的版本會寫入原始檔控制提供者中，且會成為檔案的最新版本。  
  
 您可以使用**簽入**命令來簽入檔案。 如果您利用這個命令來簽入方案或專案，也會簽入方案或專案中的所有檔案。 不過，簽入個別來源程式碼檔案，並不會簽入它所屬的專案或方案。  
  
### <a name="to-check-in-a-file"></a>簽入檔案  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下要簽入的檔案，然後按一下**簽入**。  
  
2.  如果**簽入** 對話方塊出現時，請選取適當的選項，然後按一下**確定**。  
  
     **簽入**  
     簽入所有選取的項目。  
  
     **資料行**  
     識別要顯示的資料行以及它們顯示的順序。  
  
     **註解**  
     加入與簽入作業相關聯的註解。  
  
     **簽入項目時，不要顯示簽入對話方塊**  
     簽入作業期間抑制此對話方塊。  
  
     **一般檢視**  
     在檔案的原始檔控制連接下，將您正在簽入的檔案顯示為一般清單。  
  
     **名稱**  
     顯示要簽入之項目的名稱。 項目出現時，旁邊的核取方塊會顯示為已選取。 如果您不想要簽入特定的項目，請清除它的核取方塊。  
  
     **選項。**  
     按一下按鈕右邊的箭頭之後，就會顯示原始檔控制外掛程式特定的簽入選項。  
  
     **排序**  
     排序顯示資料行的順序。  
  
     **樹狀檢視**  
     顯示您正在簽入之項目的資料夾和檔案階層。  
  
 如果您簽入的檔案不在共用的簽出中，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 環境會立即簽入這個檔案。 否則，它可能會提示您合併您的版本和其他使用者所建立的版本。  
  
## <a name="see-also"></a>另請參閱  
 [檢視修改檔案清單](../../2014/database-engine/view-a-list-of-modified-files.md)   
 [管理簽入](../../2014/database-engine/manage-checkins.md)  
  
  
