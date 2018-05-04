---
title: XQueries 處理關聯式資料 |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9367602999a0736f43e48106c5977d8abe8216c2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="xqueries-handling-relational-data"></a>XQueries 處理關聯式資料
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定針對 XQuery **xml**類型資料行或變數使用其中一種[XML 資料類型方法](../t-sql/xml/xml-data-type-methods.md)。 這些包括**query （)**， **value （)**， **exist （)**，或**modify （)**。 對查詢中所識別出的 XML 執行個體執行 XQuery，以產生 XML 。  
  
 執行 XQuery 而產生的 XML，可以包含從其他 Transact-SQL 變數或資料列集資料行擷取的值。 若要將非 XML 關聯式資料繫結到產生的 XML，SQL Server 可提供以下虛擬函數做為 XQuery 延伸模組：  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 中指定 XQuery 時，您可以使用這些 XQuery 延伸模組**query （)** 方法**xml**資料型別。 如此一來， **query （)** 方法可以產生結合 xml 與非資料的 XML-**xml**資料型別。  
  
 您也可以使用這些函式，當您使用**xml**資料類型方法**modify （)**， **value （)**， **query （)**，和**exist （)** 來公開 XML 內的關聯式值。  
  
 如需詳細資訊，請參閱[: column （） 函數 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)和[: variable （） 函數 (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 建構&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
