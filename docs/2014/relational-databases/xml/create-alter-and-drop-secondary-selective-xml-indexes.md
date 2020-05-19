---
title: 建立、修改和卸除次要選擇性 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b563b2c786f7ac1f9031dbddc4c5f343ebf688e9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717128"
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>建立、修改和卸除次要選擇性 XML 索引
  描述如何建立新的次要選擇性 XML 索引，或是修改或卸除現有的次要選擇性 XML 索引。  
  
##  <a name="creating-a-secondary-selective-xml-index"></a><a name="create"></a> 建立次要選擇性 XML 索引  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>如何：建立次要選擇性 XML 索引  
 **使用 Transact-SQL 建立次要選擇性 XML 索引**  
 透過呼叫 CREATE XML INDEX 陳述式的方式建立次要選擇性 XML 索引。 如需詳細資訊，請參閱 [建立 XML 索引 &#40;選擇性 XML 索引&#41;] （~/t-sql/statements/create-xml-index-selective-xml-indexes。  
  
 **範例**  
  
 下列範例會在 `'pathabc'`路徑上建立次要選擇性 XML 索引。 要索引的路徑是以使用 CREATE SELECTIVE XML INDEX 陳述式建立時提供的名稱識別。 如需詳細資訊，請參閱 [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-selective-xml-index-transact-sql)。  
  
```sql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="altering-a-secondary-selective-xml-index"></a><a name="alter"></a> 修改次要選擇性 XML 索引  
 次要選擇性 XML 索引不支援 ALTER 陳述式。 若要變更次要選擇性 XML 索引，請卸除現有的索引並重新建立。  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>如何：修改次要選擇性 XML 索引  
 **使用 Transact-SQL 修改次要選擇性 XML 索引**  
 1.  透過呼叫 DROP INDEX 陳述式的方式卸除現有的次要選擇性 XML 索引。 如需詳細資訊，請參閱 [DROP INDEX &#40;選擇性 XML 索引&#41;](../indexes/indexes.md)。  
  
2.  透過呼叫 CREATE XML INDEX 陳述式的方式重新建立具有所需選項的索引。 如需詳細資訊，請參閱 [建立 XML 索引 &#40;選擇性 XML 索引&#41;] （~/t-sql/statements/create-xml-index-selective-xml-indexes。  
  
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
  
  
##  <a name="dropping-a-secondary-selective-xml-index"></a><a name="drop"></a> 卸除次要選擇性 XML 索引  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>如何：卸除次要選擇性 XML 索引  
 **使用 Transact-SQL 卸除次要選擇性 XML 索引**  
 透過呼叫 DROP INDEX 陳述式的方式卸除次要選擇性 XML 索引。 如需詳細資訊，請參閱 [DROP INDEX &#40;選擇性 XML 索引&#41;](../indexes/indexes.md)。  
  
 **範例**  
  
 下列範例顯示 DROP INDEX 陳述式。  
  
```sql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [選擇性 XML 索引 &#40;SXI&#41;](selective-xml-indexes-sxi.md)  
  
  
