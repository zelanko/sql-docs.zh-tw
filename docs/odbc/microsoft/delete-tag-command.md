---
title: 刪除標記命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97ca5abca7e70f5dffdae9bf14ce64429fd203d5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303539"
---
# <a name="delete-tag-command"></a>DELETE TAG 命令
從複合索引（. cdx）檔案移除標記或標記。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>引數  
 *TagName1**CDXFileName1*[， *TagName2*[of *CDXFileName2*]] .。。  
 指定要從複合索引檔案中移除的標記。 您可以藉由包含以逗號分隔的標記名稱清單，以刪除包含一個刪除標記的多個標記。 如果開啟的索引檔案中有兩個或多個具有相同名稱的標記，您可以藉由包含*CDXFileName*，從特定的索引檔移除標記。  
  
 ALL [of *CDXFileName*]  
 從複合索引檔案中移除每個標記。 如果目前的資料表具有結構化複合索引檔案，則會從索引檔案中移除所有標記、刪除磁片中的索引檔案，以及資料表標頭中的旗標，指出相關聯的結構複合索引檔是否已移除。 使用 ALL 搭配*CDXFileName* ，從結構化複合索引檔案以外的開放式複合索引檔案移除所有標記。  
  
## <a name="remarks"></a>備註  
 以 INDEX 建立的複合索引檔案包含對應至索引項目的標記。 DELETE 標記用來從開啟的複合索引檔案移除標記或標記。 您只能刪除在目前工作區中開啟之複合索引檔案的標記。 如果您從複合索引檔案中移除所有標記，則會從磁片中刪除該檔案。  
  
 Visual FoxPro 會先查看結構化複合索引檔案中的標記（如果有開啟）。 如果標記不在結構化複合索引檔案中，則 Visual FoxPro 會在其他開啟的複合索引檔案中尋找標記。  
  
## <a name="see-also"></a>另請參閱  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
