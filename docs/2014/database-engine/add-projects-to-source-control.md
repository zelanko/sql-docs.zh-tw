---
title: 將專案加入原始檔控制 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
caps.latest.revision: 27
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2fc1ae6eadef04ee183e5551a88ed480a696cf2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148269"
---
# <a name="add-projects-to-source-control"></a>將專案加入原始檔控制中
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 方案可以主控多個指令碼專案。 您如何將專案加入原始檔控制中，會隨著專案所屬的方案是否在原始檔控制之下而不同。 如果方案在原始檔控制之下，簽入方案會自動將專案加入原始檔控制中。 如需簽入方案的詳細資訊，請參閱[檔案中檢查](../../2014/database-engine/check-in-files.md)。  
  
 如果這個專案所屬的方案不在原始檔控制之下，您可以將這個方案加入原始檔控制中，之後，便會自動加入方案的專案。 如需有關如何將解決方案新增至原始檔控制的詳細資訊，請參閱[將解決方案新增至原始檔控制](../../2014/database-engine/add-solutions-to-source-control.md)。  
  
 如果您不想將解決方案新增至原始檔控制，您可以使用**將選取範圍加入原始檔控制**命令來手動加入專案。  
  
 資料庫物件並未直接受到原始檔控制提供者的保護，但是您可以建立資料庫物件的指令碼，並在原始檔控制下儲存指令碼。  
  
### <a name="to-add-a-project-to-source-control"></a>將專案加入原始檔控制中  
  
1.  在 [方案總管] 中選取專案。  
  
2.  在上**檔案**功能表上，指向**原始檔控制**，然後按一下**將所選專案加入至原始檔控制**。  
  
    > [!NOTE]  
    >  如果您使用**將所選專案加入至原始檔控制**命令加入至原始檔控制的方案所屬的專案時，系統會提示您是否要將專案新增為子資料夾的原始檔控制解決方案，或新增專案個別資料夾中。  
  
3.  如果出現提示，請登入您的原始檔控制提供者。  
  
4.  **SourceSafe 專案中加入** 對話方塊隨即出現。 您的專案名稱會出現在**專案** 方塊中。  
  
5.  在 **資料夾**清單中，開啟您要放置您專案的資料夾。 或者，您可以按一下**Create**若要建立的資料夾中顯示的名稱**專案** 方塊中。  
  
## <a name="see-also"></a>另請參閱  
 [將方案與專案新增原始檔控制](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
