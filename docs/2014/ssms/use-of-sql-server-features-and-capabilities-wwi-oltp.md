---
title: 外部工具的引數 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2365ec137329675e2cd88e7f5bf7e1781aa3308f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280486"
---
# <a name="arguments-for-external-tools"></a>外部工具的引數
  引數是 Studio 環境提供的變數，適用於從 [工具]  功能表中啟動外部工具之時。 您可以使用 [外部工具]  對話方塊，將 [記事本] 之類的外部工具加入 [工具]  功能表中。  
  
 下表列出外部工具的引數。  
  
|名稱|引數|描述|  
|----------|--------------|-----------------|  
|**項目路徑**|$(ItemPath)|目前來源的完整檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)；如果非來源窗格在作用中，便是空白。|  
|**項目目錄**|$(ItemDir)|目前來源的目錄 (定義為磁碟機 + 路徑)；如果非來源窗格在作用中，便是空白。|  
|**項目檔案名稱**|$(ItemFilename)|目前來源的檔案名稱 (定義為檔案名稱)；如果非來源窗格在作用中，便是空白。|  
|**項目副檔名**|$(ItemExt)|目前來源的副檔名。|  
|**目前這一行** <sup>1</sup>|$(CurLine)|在編輯器中，游標所在的目前這一行位置。|  
|**目前的資料行**1|$(CurCol)|在編輯器中，游標所在的目前資料行位置。|  
|**目前的文字**1|$(CurText)|目前的文字 (在目前游標位置之下的文字，如果選擇了某單行，便是這一行)。|  
|**目標路徑**|$(TargetPath)|目標的完整檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)。|  
|**目標目錄**|$(TargetDir)|目標的目錄。|  
|**目標名稱**|$(TargetName)|目標的檔案名稱。|  
|**目標副檔名**|$(TargetExt)|目標的副檔名。|  
|**專案目錄**|$(ProjDir)|目前專案的目錄 (定義為磁碟機 + 路徑)。|  
|**專案檔案名稱**|$(ProjFileName)|目標專案的檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)。|  
|**方案目錄**|$(SolutionDir)|目前方案的目錄 (定義為磁碟機 + 路徑)。|  
|**方案檔案名稱**|$(SolutionFileName)|目標方案的檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)。|  
  
 <sup>1</sup>目前這一行、 目前的資料行或目前的文字為基礎的資料指標的位置，在文字編輯器中 [狀態] 列中所示。  
  
## <a name="see-also"></a>另請參閱  
 [外部工具對話方塊](external-tools-dialog-box.md)   
 [一般使用者介面元素](general-user-interface-elements.md)  
  
  
