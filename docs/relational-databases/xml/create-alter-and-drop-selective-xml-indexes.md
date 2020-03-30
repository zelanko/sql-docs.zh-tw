---
title: 建立、修改和卸除選擇性 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: c398f396-f630-4a2d-a264-f243c5346de1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dbfeb117d22e468bdae8b9e2ebe598b099588bfc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68112932"
---
# <a name="create-alter-and-drop-selective-xml-indexes"></a>建立、修改和卸除選擇性 XML 索引
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  描述如何建立新的選擇性 XML 索引，或是修改或卸除現有的選擇性 XML 索引。  
  
 如需選擇性 XML 索引的詳細資訊，請參閱 [選擇性 XML 索引 &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)。  
  
##  <a name="creating-a-selective-xml-index"></a><a name="create"></a> 建立選擇性 XML 索引  
  
### <a name="how-to-create-a-selective-xml-index"></a>如何：建立選擇性 XML 索引  
 **使用 Transact-SQL 建立選擇性 XML 索引**  
 透過呼叫 CREATE SELECTIVE XML INDEX 陳述式的方式建立選擇性 XML 索引。 如需詳細資訊，請參閱 [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)。  
  
 **範例**  
  
 下列範例會顯示建立選擇性 XML 索引的語法。 另外還會顯示描述要索引之路徑的多種語法變化，包含選用的最佳化提示。  
  
```sql  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()'  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
)  
```  
  
  
##  <a name="altering-a-selective-xml-index"></a><a name="alter"></a> 修改選擇性 XML 索引  
  
### <a name="how-to-alter-a-selective-xml-index"></a>如何：修改選擇性 XML 索引  
 **使用 Transact-SQL 修改選擇性 XML 索引**  
 透過呼叫 ALTER INDEX 陳述式的方式修改現有的選擇性 XML 索引。 如需詳細資訊，請參閱 [ALTER INDEX &#40;選擇性 XML 索引&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md)。  
  
 **範例**  
  
 下列範例顯示 ALTER INDEX 陳述式。 此陳述式會將路徑 `'/a/b/m'` 加入索引的 XQuery 部分，並且從 `'/a/b/e'`CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;[ 主題的範例中所建立索引的 SQL 部分刪除路徑 ](../../t-sql/statements/create-selective-xml-index-transact-sql.md)。 要刪除的路徑是以建立時提供的名稱識別。  
  
```sql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
)  
```  
  
  
##  <a name="dropping-a-selective-xml-index"></a><a name="drop"></a> 卸除選擇性 XML 索引  
  
### <a name="how-to-drop-a-selective-xml-index"></a>如何：卸除選擇性 XML 索引  
 **使用 Transact-SQL 卸除選擇性 XML 索引**  
 透過呼叫 DROP INDEX 陳述式的方式卸除選擇性 XML 索引。 如需詳細資訊，請參閱 [DROP INDEX &#40;選擇性 XML 索引&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md)。  
  
 **範例**  
  
 下列範例顯示 DROP INDEX 陳述式。  
  
```sql  
DROP INDEX sxi_index ON tbl  
```  
  
  
  
