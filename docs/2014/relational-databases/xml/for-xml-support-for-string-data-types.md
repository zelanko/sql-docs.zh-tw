---
title: 字串資料類型的 FOR XML 支援 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 268eebf7df9a0f3df31e850520baa5f24829721e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702727"
---
# <a name="for-xml-support-for-string-data-types"></a>字串資料類型的 FOR XML 支援
  實體化資料中 FOR XML 空白字元所產生的 XML。  
  
 下列範例將建立範例資料表 **T** ，並插入含有換行字元、歸位字元以及定位字元的範例資料。 SELECT 陳述式會從資料表擷取資料。  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 以下是結果：  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   在第一列所傳回的歸位字元是實體化為 &#xD。  
  
-   在第二列所傳回的定位字元是實體化為 &#x09。  
  
-   在第三列所傳回的換行字元是實體化為 &#xA。  
  
## <a name="see-also"></a>另請參閱  
 [各個 SQL Server 資料類型的 FOR XML 支援](for-xml-support-for-various-sql-server-data-types.md)  
  
  
