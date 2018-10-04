---
title: 時間戳記資料類型的 FOR XML 支援 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type
ms.assetid: 4e1920e1-e7a4-4069-965e-3f6039a6099e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 95f33ea5c042217f4d4e1fbc11353a1a2ee088b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204748"
---
# <a name="for-xml-support-for-the-timestamp-data-type"></a>Timestamp 資料類型的 FOR XML 支援
  在 FOR XML 轉換中， **timestamp** 類型值會被當作 **varbinary(8)** 資料來處理，而且一律為 Base 64 編碼。 XSD 或 XDR 結構描述 (若有要求時) 會反映此類型。  
  
```  
drop table t  
go  
create table t  
(c1 int,  
 c2 timestamp)  
go  
  
insert t values(1, null)  
go  
select * from t  
for xml auto, xmldata  
go  
```  
  
 以下是結果：  
  
```  
<Schema name="Schema1"   
        xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="t" content="empty" model="closed">  
    <AttributeType name="c1" dt:type="i4" />  
    <AttributeType name="c2" dt:type="bin.base64" />  
    <attribute type="c1" />  
    <attribute type="c2" />  
  </ElementType>  
</Schema>  
<t xmlns="x-schema:#Schema1" c1="1" c2="AAAAAAAAH04=" />  
```  
  
## <a name="see-also"></a>另請參閱  
 [各個 SQL Server 資料類型的 FOR XML 支援](for-xml-support-for-various-sql-server-data-types.md)  
  
  
