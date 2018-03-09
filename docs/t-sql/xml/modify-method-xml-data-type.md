---
title: "modify （) 方法 (xml 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 429797447e56ecb57f0dc257bfd13bea59ea1f40
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="modify-method-xml-data-type"></a>modify() 方法 (xml 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  修改 XML 文件的內容。 若要修改的內容中使用這個方法**xml**類型變數或資料行。 此方法採用 XML DML 陳述式來插入、更新或刪除 XML 資料的節點。 **Modify （)**方法**xml**資料類型僅能在 UPDATE 陳述式的 SET 子句中。  
  
## <a name="syntax"></a>語法  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>引數  
 XML_DML  
 是 XML 資料操作語言 (DML) 的字串。 XML 文件會根據此運算式來更新。  
  
> [!NOTE]  
>  如果傳回錯誤**modify （)** null 值上呼叫方法，或產生 null 值。  
  
## <a name="examples"></a>範例  
 因為**modify （)**方法需要字串中 XML 資料操作語言 (DML)，如範例**modify （)**包含在描述 XML DML 陳述式的主題。 這些範例，請參閱[insert &#40;XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)， [delete &#40;XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)和[取代的值 &#40;XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>另請參閱  
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
