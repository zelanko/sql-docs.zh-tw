---
title: 使用 BINARY BASE64 選項 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9a00e6dfd96851984018d00d017257939cb69586
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888724"
---
# <a name="use-the-binary-base64-option"></a>使用 BINARY BASE64 選項
  若查詢中指定 BINARY BASE64 選項，就會以 Base64 編碼格式傳回二進位資料。 依預設，若沒有指定 BINARY BASE64 選項，則 AUTO 模式可支援 URL 編碼的二進位資料。 也就是說，不是傳回二進位資料，而是傳回一個參考，以指向查詢執行所在之資料庫虛擬根目錄的相對 URL。 此參考可用來存取後續作業中的實際二進位資料 (使用 SQLXML ISAPI dbobject 查詢)。 此查詢必須提供足夠的資訊 (例如：主索引鍵資料行)，以便識別影像。  
  
 在指定查詢時，若將別名用於檢視的二進位資料行，就會在 URL 編碼的二進位資料中傳回該別名。 在後續動作中該別名不具任何意義，且無法使用 URL 編碼來擷取影像。 所以在利用 FOR XML AUTO 模式查詢檢視時，請勿使用別名。  
  
 例如在 SELECT 查詢中，將任何資料行轉換為二進位大型物件 (BLOB)，會使其成為遺失關聯資料表名稱與資料行名稱的暫存實體。 而這會使得 AUTO 模式查詢產生錯誤，因為查詢不知道要將此值放入 XML 階層中的哪個位置。 例如：  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 由於轉換為二進位大型物件 (BLOB)，因此查詢產生錯誤：  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 解決方法是將 BINARY BASE64 選項加入 FOR XML 子句中。 若將轉換移除，則查詢會產生預期中的結果：  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 以下是結果：  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 AUTO 模式](use-auto-mode-with-for-xml.md)  
  
  
