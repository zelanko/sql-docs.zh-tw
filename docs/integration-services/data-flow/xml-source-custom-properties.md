---
title: "XML 來源自訂屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# XML 來源自訂屬性
  XML 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 XML 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用來存取 XML 資料的模式。|  
|UseInlineSchema|布林|一個值，指出是否要使用 XML 來源中的內嵌結構描述定義。 此屬性的預設值為 **False**。|  
|XMLData|字串|要從中擷取 XML 資料的檔案或變數。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
|XMLSchemaDefinition|字串|結構描述定義檔 (.xsd) 的路徑和檔案名稱。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
  
 下表描述的是 XML 來源之輸出的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|RowsetID|字串|一個值，可識別與輸出相關聯的資料列集。|  
  
 XML 來源的輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [XML 來源](../../integration-services/data-flow/xml-source.md)。  
  
## 請參閱＜  
 [通用屬性](../Topic/Common%20Properties.md)  
  
  