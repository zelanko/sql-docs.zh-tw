---
title: 將專案加入原始檔控制 |Microsoft 文件
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
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3f0c63dec978d50ef8544c86c6cc4811f55ef195
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137418"
---
# <a name="add-projects-to-source-control"></a>將專案加入原始檔控制中
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 方案可以主控多個指令碼專案。 您如何將專案加入原始檔控制中，會隨著專案所屬的方案是否在原始檔控制之下而不同。 如果方案在原始檔控制之下，簽入方案會自動將專案加入原始檔控制中。 如需簽入方案的詳細資訊，請參閱[檔案中檢查](../../2014/database-engine/check-in-files.md)。  
  
 如果這個專案所屬的方案不在原始檔控制之下，您可以將這個方案加入原始檔控制中，之後，便會自動加入方案的專案。 如需有關將方案加入原始檔控制的詳細資訊，請參閱[將方案加入至原始檔控制](../../2014/database-engine/add-solutions-to-source-control.md)。  
  
 如果您不想要將方案加入原始檔控制，您可以使用**將選取範圍加入原始檔控制**命令來手動加入專案。  
  
 資料庫物件並未直接受到原始檔控制提供者的保護，但是您可以建立資料庫物件的指令碼，並在原始檔控制下儲存指令碼。  
  
### <a name="to-add-a-project-to-source-control"></a>將專案加入原始檔控制中  
  
1.  在 [方案總管] 中選取專案。  
  
2.  在**檔案**功能表上，指向**原始檔控制**，然後按一下 **加入所選專案加入原始檔控制**。  
  
    > [!NOTE]  
    >  如果您使用**加入所選專案加入原始檔控制**命令加入至原始檔控制的方案所屬的專案時，系統提示您是否要將專案加入原始檔控制方案的子資料夾，或新增專案做為個別的資料夾。  
  
3.  如果出現提示，請登入您的原始檔控制提供者。  
  
4.  **加入 SourceSafe 專案** 對話方塊隨即出現。 您的專案名稱會出現在**專案**方塊。  
  
5.  在**資料夾**清單中，開啟您要將您的專案的資料夾。 或者，您可以按一下**建立**建立資料夾中顯示的名稱與**專案**方塊。  
  
## <a name="see-also"></a>另請參閱  
 [將方案和專案加入原始檔控制](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  