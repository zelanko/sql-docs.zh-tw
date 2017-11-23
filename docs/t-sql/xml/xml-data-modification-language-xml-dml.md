---
title: "XML 資料修改語言 (XML DML) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: acbedcd828fcacb6b690f0380d83d7dd779f1b2e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="xml-data-modification-language-xml-dml"></a>XML 資料修改語言 (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML 資料修改語言 (XML DML) 是 XQuery 語言的延伸。 如 W3C 所定義的，XQuery 語言缺少「資料操作」(DML) 的部份。 本主題中，以及 XQuery 語言中導入的 XML DML 提供功能完整的查詢和資料修改語言，您可以使用針對**xml**資料型別。  
  
 XML DML 會將下列區分大小寫的關鍵字加入到 XQuery 中：  
  
-   **插入**  
  
-   **刪除**  
  
-   **取代值**  
  
 中所述[XML 資料類型和資料行 &#40;SQL Server &#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)，您可以建立變數和資料行**xml**輸入，並將 XML 文件或片段指派給它們。 若要修改或更新這些 XML 執行個體，請執行下列動作：  
  
-   使用[modify （) 方法的 xml 資料類型)](../../t-sql/xml/modify-method-xml-data-type.md)的**xml**資料型別。  
  
-   指定適當的 XML DML 陳述式內**modify （)**方法。  
  
 請注意，有一些屬性不能被插入、刪除或修改它們的值。 例如：  
  
-   具類型或不具型別的**xml，**屬性**xmlns**， **xmlns:\***，和**xml: base**。  
  
-   針對具類型**xml**的屬性，包括**xsi: nil**，和**xsi: type**。  
  
 其他限制包括下列項目：  
  
-   具類型或不具型別的**xml**，插入屬性**xml: base**將會失敗。  
  
-   針對具類型**xml**、 刪除和修改**xsi: nil**屬性將會失敗。 不具類型**xml**，您可以刪除屬性或修改其值。  
  
-   針對具類型**xml**、 修改值**xs: type**屬性將會失敗。 不具類型**xml**，您可以修改屬性值。  
  
 在修改具類型的 XML 執行個體時，最後的格式必須是該類型的有效執行個體。 否則，就會傳回驗證錯誤。  
  
## <a name="see-also"></a>請參閱＜  
 [insert &#40;XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)   
 [刪除 &#40;XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)   
 [取代值 &#40;XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
