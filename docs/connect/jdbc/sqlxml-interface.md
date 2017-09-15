---
title: "SQLXML 介面 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c636345439175c516b647a2951ac3bfa8824b06
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlxml-interface"></a>SQLXML 介面
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 驅動程式提供 JDBC 4.0 API 的支援，此 API 引進 java.sql.SQLXML 介面。 SQLXML 介面會定義與 XML 資料互動和進行操作的方法。 **SQLXML**資料類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml**資料型別。  
  
 SQLXML 介面會提供方法來存取 XML 值當做**字串**、**讀取器**或**寫入器**，或為**資料流**。 XML 值也可以透過存取**來源**或設為**結果**，這與搭配使用 XML 剖析器 Api，例如文件物件模型 (DOM)、 Simple API XML (SAX) 和 Streaming API for XML (StAX)，做為並使用 XSLT 轉換和 XPath。  
  
## <a name="remarks"></a>備註  
 下表將描述 SQLXML 介面中定義的方法。  
  
|方法語法|方法描述|  
|-------------------|------------------------|  
|[void free （)](http://go.microsoft.com/fwlink/?LinkId=131685)|這個方法會釋放 SQLXML 物件並且釋出它所保留的資源。|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|傳回輸入資料流，以便從 SQLXML 讀取資料。|  
|[讀取器 getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|傳回**XML**資料當做 java.io.Reader 物件或資料流的字元。|  
|[T 擴充來源 T Ierrorinfo (類別\<T > sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|傳回**來源**進行讀取**XML**值，指定由此**SQLXML**物件。<br /><br /> **注意：** Ierrorinfo 方法支援下列來源： javax.xml.transform.dom.DOMSource、 javax.xml.transform.sax.SAXSource、 javax.xml.transform.stax.StAXSource 和 java.io.InputStream。|  
|[字串 Sr](http://go.microsoft.com/fwlink/?LinkId=131757)|傳回的字串表示**XML**這個 SQLXML 物件所指定的值。|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|擷取可用來寫入的資料流**XML**這個 SQLXML 物件所代表的值。|  
|[寫入器 setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|傳回要用來寫入資料流**XML**這個 SQLXML 物件所代表的值。|  
|[T 擴充結果 T setResult (類別\<T > resultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|傳回**結果**設定**XML**值，指定由此**SQLXML**物件。<br /><br /> **注意：** setResult 方法支援下列來源： javax.xml.transform.dom.DOMResult、 javax.xml.transform.sax.SAXResult、 javax.xml.transform.stax.StaxResult 和 java.io.OutputStream。|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|設定為指定這個 SQLXML 物件所指定的 XML 值**字串**表示法。|  
  
 應用程式只能在 SQLXML 物件中讀取並寫入 XML 值一次。  
  
 Free （） 方法呼叫時，SQLXML 物件就會變成無效，無法讀取或寫入。 如果應用程式嘗試叫用該 free （） 方法以外的 SQLXML 物件上的方法時，會擲回例外狀況。  
  
 在 SQLXML 物件變成無法讀取或寫入應用程式會呼叫任何下列的 getter 方法時： Ierrorinfo getCharacterStream，getBinaryStream，和 getString。  
  
 SQLXML 物件就無法寫入或讀取應用程式會呼叫任何下列的 setter 方法時： setResult setCharacterStream、 setBinaryStream、 和 setString。  
  
## <a name="see-also"></a>另請參閱  
 [支援 XML 資料](../../connect/jdbc/supporting-xml-data.md)  
  
  
