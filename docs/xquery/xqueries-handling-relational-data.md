---
title: Xquery 處理關聯式資料 |Microsoft Docs
description: 瞭解如何使用 XQuery extension sql： column （）和 sql： variable （），將非 XML 關聯式資料系結至 XML。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ebd9c4d2bae1c491d2bd7a23e52c83457942fb6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775473"
---
# <a name="xqueries-handling-relational-data"></a>XQueries 處理關聯式資料
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  您可以使用其中一種[Xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)，針對**xml**類型資料行或變數指定 XQuery。 這些包括**query （）**、 **value （）**、**存在（）** 或**modify （）**。 對查詢中所識別出的 XML 執行個體執行 XQuery，以產生 XML 。  
  
 執行 XQuery 而產生的 XML，可以包含從其他 Transact-SQL 變數或資料列集資料行擷取的值。 若要將非 XML 關聯式資料繫結到產生的 XML，SQL Server 可提供以下虛擬函數做為 XQuery 延伸模組：  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 在**xml**資料類型的**query （）** 方法中指定 xquery 時，您可以使用這些 xquery 延伸模組。 因此， **query （）** 方法可以產生結合 xml 和非**XML**資料類型之資料的 XML。  
  
 您也可以在使用**xml**資料類型方法**modify （）**、 **value （）**、 **query （）** 和**存在（）** 時，使用這些函數來公開 xml 內的關聯式值。  
  
 如需詳細資訊，請參閱[sql： column （）函數（xquery）](../xquery/xquery-extension-functions-sql-column.md)和[sql： variable （）函數（xquery）](../xquery/xquery-extension-functions-sql-variable.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [&#40;XQuery&#41;的 XML 結構](../xquery/xml-construction-xquery.md)  
  
  
