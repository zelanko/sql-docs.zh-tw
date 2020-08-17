---
description: DELETE TAG 命令
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
ms.openlocfilehash: 16eeedd8d9995cf636791688179ba21002411aea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340884"
---
# <a name="delete-tag-command"></a>DELETE TAG 命令
 ( cdx) 檔中，移除複合索引的標記或標記。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>引數  
 *TagName1*Of *CDXFileName1*[， *TagName2*[of *CDXFileName2*]] .。。  
 指定要從複合索引檔案中移除的標記。 您可以藉由包含以逗號分隔的標籤名稱清單，以一個刪除標記刪除多個標記。 如果開啟的索引檔案中有兩個或多個具有相同名稱的標記，您可以藉由包含 *CDXFileName*，從特定的索引檔中移除標記。  
  
 ALL [of *CDXFileName*]  
 從複合索引檔案中移除每個標記。 如果目前的資料表具有結構化複合索引檔案，則會從索引檔中移除所有標記，並從磁片中刪除索引檔案，而且會移除資料表標頭中的旗標，指出已移除相關聯的結構化複合索引檔案。 使用 ALL with with *CDXFileName* ，從結構化複合索引檔案以外的開啟複合索引檔案中移除所有標記。  
  
## <a name="remarks"></a>備註  
 以 INDEX 建立的複合索引檔案包含對應至索引項目的標記。 DELETE 標記是用來從開啟的複合索引檔中移除標記或標記。 您只能刪除在目前工作區中開啟之複合索引檔案的標記。 如果您從複合索引檔案中移除所有標記，就會從磁片中刪除該檔案。  
  
 Visual FoxPro 會先查看結構化複合索引檔案中的標記 (如果有開啟) 。 如果標記不在結構化複合索引檔案中，Visual FoxPro 接著會在其他開啟的複合索引檔案中尋找標記。  
  
## <a name="see-also"></a>另請參閱  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
