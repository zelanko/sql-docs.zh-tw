---
title: 移動或刪除項目或專案 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-solutions
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96e5484ed59b0852f0099602b5a4e3ff359d1b6f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="remove-or-delete-an-item-or-project"></a>移除或刪除項目或專案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 專案中的專案項目有「查詢」、「連接」及「其他」檔案。 您可以在不從儲存體清除檔案的情況下，從方案中移除專案查詢和其他檔案。 當專案或項目在目前的方案中沒有用，而且您想要將它包含在另一個方案中時，就可移除它。  
  
### <a name="to-remove-a-project-item"></a>移除專案項目  
  
1.  在 [方案總管] 中，選取您要移除的專案項目。  
  
2.  在 [編輯] 功能表上，按一下 [移除]。  
  
3.  在確認對話方塊中，按一下 [移除]，從專案中移除項目。  
  
移除的項目仍會在檔案系統中。 因此，您可以將已移除的項目加入原始方案或另一個方案中。  
  
#### <a name="to-remove-a-project"></a>移除專案  
  
1.  在 [方案總管] 中，選取您要移除的專案。  
  
2.  在 [編輯] 功能表上，按一下 [移除]。  
  
3.  在確認對話方塊中，按一下 [確定]，從方案中移除專案。  
  
您可以永久刪除專案，但您必須先從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 方案中，移除任何指向這個專案的參考，之後，再利用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 檔案總管，從儲存體中，永久刪除相關的檔案。  
  
#### <a name="to-delete-a-project"></a>刪除專案  
  
1.  在 [方案總管] 中，移除您要從方案中刪除的專案。  
  
2.  在 Windows 的 [檔案總管] 中，尋找和選取您要刪除的專案或項目的相關檔案。  
  
3.  在 [檔案] 功能表上，按一下 [刪除]。  
  
## <a name="see-also"></a>另請參閱  
[方案總管](../../ssms/solution/solution-explorer.md)  
[將新項目加入專案](../../ssms/solution/add-new-items-to-a-project.md)  
[將現有的項目加入至專案](../../ssms/solution/add-existing-items-to-a-project.md)  
  
