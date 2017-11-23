---
title: "刪除標記命令 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e31cf41163f512b5450e5452f8e0adff5c0a604
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="delete-tag-command"></a>刪除標記命令
從複合的索引 (.cdx) 檔案中移除標記。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>引數  
 *TagName1*OF *CDXFileName1*[， *TagName2*[OF *CDXFileName2*]]...  
 指定要移除的複合索引檔案的標籤。 您可以包括一份以逗號分隔的標記名稱，以刪除標記刪除多個標記。 如果具有相同名稱的兩個或多個標記存在於開啟索引檔案，您可以移除標記特定索引檔案所包含的*CDXFileName*。  
  
 所有 [OF *CDXFileName*]  
 移除是複合的索引檔中的每個標記。 如果目前的資料表結構的複合索引檔案，會從索引檔案中移除所有標記，索引會刪除該檔案從磁碟，並指出相關聯的結構複合索引檔案存在的資料表的標頭中的旗標都移除。 使用所有的 OF *CDXFileName*移除從開啟的複合索引檔案結構複合的索引檔以外的所有標記。  
  
## <a name="remarks"></a>備註  
 索引，以建立的複合索引檔案可以包含對應到索引項的標記。 刪除標記用來從開啟的複合索引檔案移除標記。 您可以刪除只有標記從複合的索引在目前的工作區中開啟的檔案。 如果您從是複合的索引檔移除所有標記，會從磁碟刪除檔案。  
  
 Visual FoxPro 會尋找第一個結構複合的索引檔中的標記 （如果有開啟）。 如果標記未結構化的複合索引檔中，Visual FoxPro 接著會尋找其他開啟的複合索引檔案中的標記。  
  
## <a name="see-also"></a>請參閱＜  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
