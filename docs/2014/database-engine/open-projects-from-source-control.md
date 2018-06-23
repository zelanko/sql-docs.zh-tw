---
title: 從原始檔控制中開啟專案 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- projects [SQL Server Management Studio], opening
- opening projects
ms.assetid: 942f93a3-e264-4ec4-ba72-a28e0509a527
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0963ef46d2378cd23eae5c1cec23b76c0919e3d1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137129"
---
# <a name="open-projects-from-source-control"></a>從原始檔控制開啟專案
  您可以利用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，直接從原始檔控制中開啟專案。 當您執行這個動作時，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會擷取專案的最新版本，將它複製到本機磁碟中。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境也會自動建立一項專案的方案。  
  
 從原始檔控制中開啟專案之後，您便可以簽出和修改專案檔。  
  
> [!NOTE]  
>  下列程序只應使用一次。 之後，您應該開啟像任何其他專案的專案 (按一下**檔案**，**開啟**，然後**專案**)。  
  
### <a name="to-open-a-project-from-source-control"></a>從原始檔控制中開啟專案  
  
1.  在**檔案**功能表上，指向**原始檔控制**，然後按一下**從原始檔控制開啟**。  
  
2.  如果出現提示，請登入 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe。  
  
3.  在**從 SourceSafe 建立本機專案**對話方塊方塊中，開啟包含要開啟專案的資料夾。  
  
4.  **資料夾中建立新的專案**方塊來識別這個專案將建立的本機目錄的變更。 如果您想要將專案放在不同的目錄中，輸入路徑的目錄或使用**瀏覽**按鈕，以找出您的本機磁碟上的目錄。  
  
5.  在**在資料夾中建立新的專案**，確認正確的資料夾隨即顯示，然後按一下**確定**。  
  
6.  在**開啟方案**對話方塊方塊中，選取您想要開啟，然後按一下 的專案**開啟**。  
  
## <a name="see-also"></a>另請參閱  
 [從原始檔控制開啟方案和專案](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)   
 [從原始檔控制開啟方案](../../2014/database-engine/open-solutions-from-source-control.md)  
  
  