---
description: modify() 方法 (xml 資料類型)
title: modify() 方法 (xml 資料類型)
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 56037b1a9caf1c6b37c62e0bdb10ecbf76c045a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496357"
---
# <a name="modify-method-xml-data-type"></a>modify() 方法 (xml 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  修改 XML 文件的內容。 使用此方法來修改 **xml** 類型變數或資料行的內容。 此方法採用 XML DML 陳述式來插入、更新或刪除 XML 資料的節點。 **xml** 資料類型的 **modify()** 方法只能用在 UPDATE 陳述式的 SET 子句中。  
  
## <a name="syntax"></a>語法  
  
```  
  
modify (XML_DML)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

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
  
  
