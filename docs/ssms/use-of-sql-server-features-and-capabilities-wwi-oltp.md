---
title: 外部工具的引數 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b1f1cff589dfe005011c025b6083821d259f6e9f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267056"
---
# <a name="arguments-for-external-tools"></a>外部工具的引數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
引數是 Studio 環境提供的變數，適用於從 [工具]  功能表中啟動外部工具之時。 您可以使用 [外部工具]  對話方塊，將 [記事本] 之類的外部工具加入 [工具]  功能表中。  
  
下表列出外部工具的引數。  
  
|[屬性]|引數|Description|  
|--------|------------|---------------|  
|**項目路徑**|$(ItemPath)|目前來源的完整檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)；如果非來源窗格在作用中，便是空白。|  
|**項目目錄**|$(ItemDir)|目前來源的目錄 (定義為磁碟機 + 路徑)；如果非來源窗格在作用中，便是空白。|  
|**項目檔案名稱**|$(ItemFilename)|目前來源的檔案名稱 (定義為檔案名稱)；如果非來源窗格在作用中，便是空白。|  
|**項目副檔名**|$(ItemExt)|目前來源的副檔名。|  
|**目前行***|$(CurLine)|在編輯器中，游標所在的目前這一行位置。|  
|**目前的資料行***|$(CurCol)|在編輯器中，游標所在的目前資料行位置。|  
|**目前的文字***|$(CurText)|目前的文字 (在目前游標位置之下的文字，如果選擇了某單行，便是這一行)。|  
|**目標路徑**|$(TargetPath)|目標的完整檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)。|  
|**目標目錄**|$(TargetDir)|目標的目錄。|  
|**目標名稱**|$(TargetName)|目標的檔案名稱。|  
|**目標副檔名**|$(TargetExt)|目標的副檔名。|  
|**專案目錄**|$(ProjDir)|目前專案的目錄 (定義為磁碟機 + 路徑)。|  
|**專案檔案名稱**|$(ProjFileName)|目標專案的檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)。|  
|**方案目錄**|$(SolutionDir)|目前方案的目錄 (定義為磁碟機 + 路徑)。|  
|**方案檔案名稱**|$(SolutionFileName)|目標方案的檔案名稱 (定義為磁碟機 + 路徑 + 檔案名稱)。|  
  
*目前這一行、目前的資料行或目前的文字，是依狀態列所顯示，以文字編輯器中的游標位置為基礎。  
  
## <a name="see-also"></a>另請參閱  
[外部工具對話方塊](../ssms/external-tools-dialog-box.md)  
[一般使用者介面元素](../ssms/general-user-interface-elements.md)  
  
