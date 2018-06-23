---
title: 移動或刪除項目或專案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7834be297cef98d18f78d74999750bf347454bb9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135059"
---
# <a name="remove-or-delete-an-item-or-project"></a>移除或刪除項目或專案
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 專案中的專案項目有「查詢」、「連接」及「其他」檔案。 您可以在不從儲存體清除檔案的情況下，從方案中移除專案查詢和其他檔案。 當專案或項目在目前的方案中沒有用，而且您想要將它包含在另一個方案中時，就可移除它。  
  
### <a name="to-remove-a-project-item"></a>移除專案項目  
  
1.  在 [方案總管] 中，選取您要移除的專案項目。  
  
2.  在 [編輯] 功能表上，按一下 [移除]。  
  
3.  在確認對話方塊中，按一下 [移除]，從專案中移除項目。  
  
 移除的項目仍會在檔案系統中。 因此，您可以將已移除的項目加入原始方案或另一個方案中。  
  
#### <a name="to-remove-a-project"></a>移除專案  
  
1.  在 [方案總管] 中，選取您要移除的專案。  
  
2.  在 [編輯] 功能表上，按一下 [移除]。  
  
3.  在確認對話方塊中，按一下 [確定]，從方案中移除專案。  
  
 您可以永久刪除專案，但您必須先從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 方案中，移除任何指向這個專案的參考，之後，再利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 檔案總管，從儲存體中，永久刪除相關的檔案。  
  
#### <a name="to-delete-a-project"></a>刪除專案  
  
1.  在 [方案總管] 中，移除您要從方案中刪除的專案。  
  
2.  在 Windows 的 [檔案總管] 中，尋找和選取您要刪除的專案或項目的相關檔案。  
  
3.  在 [檔案] 功能表上，按一下 [刪除]。  
  
## <a name="see-also"></a>另請參閱  
 [方案總管](solution-explorer.md)   
 [將新的項目加入至專案](add-new-items-to-a-project.md)   
 [將現有的項目加入至專案](add-existing-items-to-a-project.md)  
  
  