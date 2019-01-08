---
title: DELETE TAG 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eabecbc399751f03e9e5c25b32423ce0839072dc
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207747"
---
# <a name="delete-tag-command"></a>DELETE TAG 命令
從複合的索引 (.cdx) 檔案中移除的標記。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>引數  
 *TagName1*OF *CDXFileName1*[， *TagName2*[OF *CDXFileName2*]]...  
 指定標籤上，從複合的索引檔中移除。 您可以包括一份以逗號分隔的標記名稱，以刪除標記刪除多個標記。 如果具有相同名稱的兩個或多個標記存在於開啟索引檔案，您可以移除標記從特定索引的檔案包括 OF *CDXFileName*。  
  
 所有 [OF *CDXFileName*]  
 移除是複合的索引檔中的每個標記。 如果目前的資料表有結構化的複合索引檔案，會從索引檔案中移除所有標記、 索引檔案會從磁碟、 刪除和指出相關聯的結構化複合索引檔案存在的資料表的標頭中的旗標會都移除。 所有搭配 OF *CDXFileName*移除從開啟的複合索引檔案結構複合的索引檔以外的所有標記。  
  
## <a name="remarks"></a>備註  
 索引，以建立的複合的索引檔案包含對應到索引項的標記。 刪除標記用來從開啟的複合索引檔案中移除的標記。 您可以刪除僅標記，從複合的索引在目前的工作區中開啟的檔案。 如果您移除所有標記從複合的索引檔案時，會從磁碟刪除檔案。  
  
 Visual FoxPro 會尋找第一個標籤中的結構化的複合索引檔案 （如果有開啟）。 如果標記不在結構化的複合索引檔案，Visual FoxPro 接著會尋找其他開啟的複合索引檔案中的標記。  
  
## <a name="see-also"></a>另請參閱  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
