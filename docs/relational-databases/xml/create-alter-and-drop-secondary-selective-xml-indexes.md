---
title: "建立、修改和卸除次要選擇性 XML 索引 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0404369cf79e3e74b65aeb3074f6232e3245f45b
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>建立、修改和卸除次要選擇性 XML 索引
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 描述如何建立新的次要選擇性 XML 索引，或是改變或卸除現有的次要選擇性 XML 索引。  
  
##  <a name="create"></a> 建立次要選擇性 XML 索引  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>如何：建立次要選擇性 XML 索引  
 **使用 Transact-SQL 建立次要選擇性 XML 索引**  
 透過呼叫 CREATE XML INDEX 陳述式的方式建立次要選擇性 XML 索引。 如需詳細資訊，請參閱 [CREATE XML INDEX &#40;選擇性 XML 索引&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)。  
  
 **範例**  
  
 下列範例會在 `'pathabc'`路徑上建立次要選擇性 XML 索引。 要索引的路徑是以使用 CREATE SELECTIVE XML INDEX 陳述式建立時提供的名稱識別。 如需詳細資訊，請參閱 [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)。  
  
```sql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="alter"></a> 修改次要選擇性 XML 索引  
 次要選擇性 XML 索引不支援 ALTER 陳述式。 若要變更次要選擇性 XML 索引，請卸除現有的索引並重新建立。  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>如何：修改次要選擇性 XML 索引  
 **使用 Transact-SQL 修改次要選擇性 XML 索引**  
 1.  透過呼叫 DROP INDEX 陳述式的方式卸除現有的次要選擇性 XML 索引。 如需詳細資訊，請參閱 [DROP INDEX &#40;選擇性 XML 索引&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md)。  
  
2.  透過呼叫 CREATE XML INDEX 陳述式的方式重新建立具有所需選項的索引。 如需詳細資訊，請參閱 [CREATE XML INDEX &#40;選擇性 XML 索引&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)。  
  
 **範例**  
  
 下列範例會藉由卸除次要選擇性 XML 索引並重新建立的方式進行變更。  
  
```sql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="drop"></a> 卸除次要選擇性 XML 索引  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>如何：卸除次要選擇性 XML 索引  
 **使用 Transact-SQL 卸除次要選擇性 XML 索引**  
 透過呼叫 DROP INDEX 陳述式的方式卸除次要選擇性 XML 索引。 如需詳細資訊，請參閱 [DROP INDEX &#40;選擇性 XML 索引&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md)。  
  
 **範例**  
  
 下列範例顯示 DROP INDEX 陳述式。  
  
```sql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [選擇性 XML 索引 &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
