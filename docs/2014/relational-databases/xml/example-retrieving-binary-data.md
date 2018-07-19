---
title: 範例：擷取二進位資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4200917619f7b36f34d39754cc548a5a3cb3458
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280764"
---
# <a name="example-retrieving-binary-data"></a>範例：擷取二進位資料
  下列查詢會傳回儲存在 `varbinary(max)` 類型資料行中的產品相片。 在查詢中指定 `BINARY BASE64` 選項，以便將二進位資料透過 Base64 編碼格式傳回。  
  
## <a name="example"></a>範例  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM Production.ProductPhoto  
WHERE ProductPhotoID=1  
FOR XML RAW, BINARY BASE64 ;  
GO  
```  
  
 以下是結果：  
  
```  
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR XML 的 RAW 模式](use-raw-mode-with-for-xml.md)  
  
  
