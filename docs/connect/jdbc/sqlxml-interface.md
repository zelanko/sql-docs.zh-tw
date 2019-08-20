---
title: SQLXML 介面 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72cccce89d5e30a92f38b956c8b7996949d3bb46
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027694"
---
# <a name="sqlxml-interface"></a>SQLXML 介面

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

JDBC 驅動程式提供 JDBC 4.0 API 的支援，此 API 引進 java.sql.SQLXML 介面。 SQLXML 介面會定義與 XML 資料互動和進行操作的方法。 **SQLXML**資料類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xml**資料類型。  
  
SQLXML 介面提供將 XML 值當做**字串**、**讀取器**或**寫入器**或**資料流程**來存取的方法。 XML 值也可以透過 **Source** 存取或設定為 **Result**，以便搭配文件物件模型 (DOM)、Simple API for XML (SAX) 和 Streaming API for XML (StAX) 等 XML 剖析器 API 以及 XSLT 轉換和 XPath 使用。  
  
## <a name="remarks"></a>備註  

下表將描述 SQLXML 介面中定義的方法。  
  
|方法語法|方法描述|  
|-------------------|------------------------|  
|[void free()](https://go.microsoft.com/fwlink/?LinkId=131685)|這個方法會釋放 SQLXML 物件並且釋出它所保留的資源。|  
|[InputStream getBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131754)|傳回輸入資料流，以便從 SQLXML 讀取資料。|  
|[Reader getCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131755)|傳回 **XML** 資料當作 java.io.Reader 物件或字元資料流。|  
|[T extends Source T getSource(Class\<T> sourceClass)](https://go.microsoft.com/fwlink/?LinkId=131756)|傳回讀取這個**SQLXML**物件所指定之**XML**值的**來源**。<br /><br /> **注意：** getSource 方法支援下列來源：javax.xml.transform.dom.DOMSource、javax.xml.transform.sax.SAXSource、javax.xml.transform.stax.StAXSource 和 java.io.InputStream。|  
|[String getString()](https://go.microsoft.com/fwlink/?LinkId=131757)|傳回這個 SQLXML 物件所指定之 **XML** 值的字串表示法。|  
|[OutputStream setBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131758)|擷取可用來寫入這個 SQLXML 物件所代表之 **XML** 值的資料流。|  
|[Writer setCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131759)|傳回要用來寫入這個 SQLXML 物件所代表之 **XML** 值的資料流。|  
|[T extends Result T setResult(Class\<T> resultClass)](https://go.microsoft.com/fwlink/?LinkId=131760)|傳回設定此**SQLXML**物件所指定之**XML**值的**結果**。<br /><br /> **注意：** setResult 方法支援下列來源：javax.xml.transform.dom.DOMResult、javax.xml.transform.sax.SAXResult、javax.xml.transform.stax.StaxResult 和 java.io.OutputStream。|  
|[void setString(String value)](https://go.microsoft.com/fwlink/?LinkId=131762)|將這個 SQLXML 物件所指定的 XML 值設定為指定的 **String** 表示法。|  
  
應用程式只能在 SQLXML 物件中讀取並寫入 XML 值一次。  
  
呼叫 free() 方法時，SQLXML 物件就會變成無效，而且無法讀取或寫入。 如果應用程式嘗試針對該 SQLXML 物件呼叫 free() 方法以外的方法，就會擲回例外狀況。  
  
當應用程式呼叫下列任何 getter 方法時, SQLXML 物件就不會變成可讀取或可寫入: getSource、getCharacterStream、getBinaryStream 和 getString。  
  
當應用程式呼叫下列任何 setter 方法時, SQLXML 物件就不會成為可寫入或不可讀取的: setResult、setCharacterStream、setBinaryStream 和 setString。  
  
## <a name="see-also"></a>另請參閱  

[支援 XML 資料](../../connect/jdbc/supporting-xml-data.md)  
