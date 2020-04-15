---
title: 刪除 TAG 指令 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303539"
---
# <a name="delete-tag-command"></a>DELETE TAG 命令
從複合索引 (.cdx) 檔案中刪除標記或標記。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>引數  
 *標籤名稱1**CDXFilename1*[,*標籤名稱2* *[CDXFilename2]...*  
 指定要從複合索引檔中刪除的標記。 您可以通過包含用逗號分隔的標記名稱列表來刪除具有一個 DELETE TAG 的多個標記。 如果打開索引檔中存在兩個或多個同名標記,則可以通過包括 OF *CDXFileName*來從特定索引檔中刪除標記。  
  
 所有 *[CDX 檔案名稱 ]*  
 從複合索引檔中刪除每個標記。 如果當前表具有結構複合索引檔,則從索引檔中刪除所有標記,從磁盤中刪除索引檔,刪除表標頭中指示存在關聯結構複合索引檔的標誌。 將 ALL 與 OF *CDXFileName*一起使用,從打開的複合索引檔中刪除結構複合索引檔以外的所有標記。  
  
## <a name="remarks"></a>備註  
 使用 INDEX 創建的複合索引檔包含與索引項目對應的標記。 刪除標籤用於從打開的複合索引檔中刪除標記或標記。 您只能從目前工作區中打開的複合索引檔中刪除標記。 如果從複合索引檔中刪除所有標記,則該檔將從磁盤中刪除。  
  
 Visual FoxPro 首先查找結構複合索引檔中的標記(如果一個已打開)。 如果標記不在結構複合索引檔中,Visual FoxPro 然後在其他打開的複合索引檔中尋找標記。  
  
## <a name="see-also"></a>另請參閱  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
