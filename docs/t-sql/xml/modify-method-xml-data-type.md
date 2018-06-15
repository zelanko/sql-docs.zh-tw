---
title: modify() 方法 (xml 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 01ad2afc24c09cdd6a05189335f1e0d6827d24c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33067385"
---
# <a name="modify-method-xml-data-type"></a>modify() 方法 (xml 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  修改 XML 文件的內容。 使用此方法來修改 **xml** 類型變數或資料行的內容。 此方法採用 XML DML 陳述式來插入、更新或刪除 XML 資料的節點。 **xml** 資料類型的 **modify()** 方法只能用在 UPDATE 陳述式的 SET 子句中。  
  
## <a name="syntax"></a>語法  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>引數  
 XML_DML  
 是 XML 資料操作語言 (DML) 的字串。 XML 文件會根據此運算式來更新。  
  
> [!NOTE]  
>  如果對 Null 值或 Null 值的結果呼叫 **modify()** 方法，會傳回錯誤。  
  
## <a name="examples"></a>範例  
 因為 **modify()** 方法需要 XML 資料操作語言 (DML) 中的字串，所以 **modify()** 的範例包含在描述 XML DML 陳述式的主題中。 如需這些範例，請參閱 [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md)、[delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md) 和 [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
