---
title: 從原始檔控制中排除檔案 |Microsoft 文件
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
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 597be5211a36e42320f3f7601c052121ef8aa2a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133771"
---
# <a name="exclude-files-from-source-control"></a>從原始檔控制中排除檔案
  如果您正在使用的方案包含不需要原始檔控制服務的檔案，您可以使用**從原始檔控制排除**命令，從原始檔控制中排除的檔案。 當您執行這個動作時，檔案會保留在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 資料庫中，但不會再隨著專案而簽入或簽出。  
  
 您應該使用**從原始檔控制排除**命令只有在產生的檔案。 產生的檔案是可以完全重新建立[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]根據方案中的另一個檔案的內容。  
  
### <a name="to-exclude-a-file-from-source-control"></a>從原始檔控制中排除檔案  
  
1.  在 [方案總管] 中，選取要排除的檔案。  
  
2.  在**檔案**功能表上，指向**原始檔控制**，然後按一下 **排除** *\<檔案名稱 >* **從原始檔控制**。  
  
## <a name="see-also"></a>另請參閱  
 [原始檔控制基本概念](../../2014/database-engine/source-control-basics.md)   
 [設定原始檔控制選項](../../2014/database-engine/set-source-control-options.md)   
 [變更原始檔控制連接](../../2014/database-engine/change-source-control-connections.md)  
  
  