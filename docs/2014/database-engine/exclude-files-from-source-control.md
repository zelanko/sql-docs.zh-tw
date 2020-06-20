---
title: 從原始檔控制排除檔案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9fb3c5ccb4fcaad062236eec6d04f995557dc2b8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933086"
---
# <a name="exclude-files-from-source-control"></a>從原始檔控制中排除檔案
  如果您處理的方案包含不需要原始檔控制服務的檔案，您可以使用 [**從原始檔控制排除**] 命令，將檔案從原始檔控制中排除。 當您執行這個動作時，檔案會保留在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 資料庫中，但不會再隨著專案而簽入或簽出。  
  
 您應該只在產生的檔案上使用 [**從原始檔控制排除**] 命令。 產生的檔案是可以 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 根據方案中另一個檔案的內容，完全重新建立的檔案。  
  
### <a name="to-exclude-a-file-from-source-control"></a>從原始檔控制中排除檔案  
  
1.  在 [方案總管] 中，選取要排除的檔案。  
  
2.  **在 [檔案**] 功能表上，指向 [原始檔**控制**]，然後按一下 [ **Exclude** *\<file name>* **從原始檔控制**排除]。  
  
## <a name="see-also"></a>另請參閱  
 [原始檔控制基本概念](../../2014/database-engine/source-control-basics.md)   
 [設定原始檔控制選項](../../2014/database-engine/set-source-control-options.md)   
 [變更原始檔控制連接](../../2014/database-engine/change-source-control-connections.md)  
  
  
