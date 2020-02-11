---
title: 將版本指定為最新版本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], latest version
- latest file version specified
- file versions [SQL Server]
ms.assetid: 407dffb1-3ecf-461e-835d-124781f26ee7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f34631e979ded7a329939c23a758ccc0c9aea959
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62773474"
---
# <a name="specify-a-version-as-the-latest-version"></a>將版本指定為最新版
  當您將檔案簽入原始檔控制中，簽入的版本會成為最新的版本；簽出或擷取最新版本的使用者會收到最近簽入之項目的本機副本。  
  
 不過，在某些狀況下，您可能會想指定項目較早的版本來做為最新的版本。 例如，您簽出檔案，並修改檔案，然後再簽入檔案。 稍後決定捨棄您進行的修改。 由於您已簽入這個項目，您無法恢復原來的簽出項目。 在這個狀況下，您可以將原來簽出的版本指定為項目的最新版本。  
  
 您可以利用下列方式來指定最新的版本：  
  
-   **釘選版本**。 當您固定某個檔案版本時，並不會刪除比固定版本還新的版本。 另外，您也可以取消固定先前所固定的檔案。 當您執行這個動作時，最近簽入的檔案版本會成為最新的版本。 不過，您無法簽出固定的檔案。  
  
-   回復**到指定的版本**。 當您回復到指定的版本時，會從原始檔控制中刪除比回復目標版本還新的所有版本。 之後，您可以簽出其餘的最新版本。  
  
### <a name="to-pin-a-version"></a>固定版本  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，開啟方案。  
  
2.  在 [方案總管] 中，選取您要指定為最新版本的檔案。  
  
3.  **在 [檔案**] 功能表上，指向 [原始檔**控制**]，然後按一下 [ **ViewHistory**]。  
  
4.  在 [ **** \<檔> 的歷程記錄] 對話方塊中，選取您要指定為最新的版本，然後按一下 [**釘**選]。  
  
     此時所選版本旁會出現圖釘符號，表示它是目前的檔案版本。 如果 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 載入了不同的版本，系統會提示您重新載入檔案。  
  
### <a name="to-roll-back-to-a-version"></a>回復到某個版本  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，開啟方案。  
  
2.  在 [方案總管] 中，選取您要指定為最新版本的項目。  
  
3.  **在 [檔案**] 功能表上，指向 [原始檔**控制**]，然後按一下 [歷程**記錄**]。  
  
4.  在 [**記錄選項**] 對話方塊中，按一下 **[確定**] 以顯示 [檔案的歷程**記錄**] 對話方塊。  
  
5.  在 [檔案的歷程**記錄**] 方塊中，選取您要指定為最新版本的版本，然後按一下 [**復原**]。  
  
     此時會出現一則訊息，通知您將刪除所選版本之後的所有版本。  
  
6.  按一下 **[是]** ，回復到選取的版本。  
  
## <a name="see-also"></a>另請參閱  
 [管理簽入](../../2014/database-engine/manage-checkins.md)   
 [簽入檔案](../../2014/database-engine/check-in-files.md)  
  
  
