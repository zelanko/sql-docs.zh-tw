---
title: 將專案加入至原始檔控制 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0936af9b97d08c6bcd5033e61d9fa1c9153272e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62791758"
---
# <a name="add-projects-to-source-control"></a>將專案加入原始檔控制中
  
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 方案可以主控多個指令碼專案。 您如何將專案加入原始檔控制中，會隨著專案所屬的方案是否在原始檔控制之下而不同。 如果方案在原始檔控制之下，簽入方案會自動將專案加入原始檔控制中。 如需簽入方案的詳細資訊，請參閱[簽入](../../2014/database-engine/check-in-files.md)檔案。  
  
 如果這個專案所屬的方案不在原始檔控制之下，您可以將這個方案加入原始檔控制中，之後，便會自動加入方案的專案。 如需將方案加入至原始檔控制的詳細資訊，請參閱[將方案加入至原始檔控制](../../2014/database-engine/add-solutions-to-source-control.md)。  
  
 如果您不想要將方案加入至原始檔控制，可以使用 [**將選取專案加入至原始檔控制**] 命令來手動加入專案。  
  
 資料庫物件並未直接受到原始檔控制提供者的保護，但是您可以建立資料庫物件的指令碼，並在原始檔控制下儲存指令碼。  
  
### <a name="to-add-a-project-to-source-control"></a>將專案加入原始檔控制中  
  
1.  在 [方案總管] 中選取專案。  
  
2.  **在 [檔案**] 功能表上，指向 [原始檔**控制**]，然後按一下 [**將選取的專案加入至原始檔控制**]。  
  
    > [!NOTE]  
    >  如果您使用 [**將選取的專案加入至原始檔控制**] 命令來加入屬於原始檔控制方案的專案，系統會提示您是否要將專案加入至原始檔控制方案的子資料夾，或加入專案做為個別的資料夾。  
  
3.  如果出現提示，請登入您的原始檔控制提供者。  
  
4.  [**加入至 SourceSafe 專案**] 對話方塊隨即出現。 專案的名稱會出現在 [**專案**] 方塊中。  
  
5.  在 [**資料夾**] 清單中，開啟您要放置專案的資料夾。 或者，您也可以按一下 [**建立**]，以在 [**專案**] 方塊中顯示名稱來建立資料夾。  
  
## <a name="see-also"></a>另請參閱  
 [將方案與專案加入原始檔控制](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
