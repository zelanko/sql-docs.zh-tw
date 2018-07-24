---
title: xml_schema_namespace (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a459c3df3d4ee716a89a54ebc70ee2132183ee4c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038006"
---
# <a name="xmlschemanamespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在指定的 XML 結構描述集合中重新建構所有結構描述或特定結構描述。 這個函數會傳回 **xml** 資料類型執行個體。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>引數  
 *Relational_schema*  
 這是關聯式結構描述名稱。 *Relational_schema* 是 **sysname**。  
  
 *XML_schema_collection_name*  
 這是要重新建構的 XML 結構描述集合名稱。 *XML_schema_collection_name* 是 **sysname**。  
  
 *命名空間*  
 這是您要重新建構之 XML 結構描述的命名空間 URI。 它限制為 1,000 個字元。 如果不提供命名空間 URI，會重新建構整個 XML 結構描述集合。 *Namespace* 是 **nvarchar(4000)**。  
  
## <a name="return-types"></a>傳回類型  
 **xml**  
  
## <a name="remarks"></a>Remarks  
 當您使用 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) 或 [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) 在資料庫中匯入 XML 結構描述元件時，會保留用於驗證的結構描述部份。 因此，重新建構的結構描述與原始結構描述文件可能不會逐字相同。 尤其，會失去註解 (Annotation)、空白和註解 (Comment)；且隱含的類型資訊會變成明確資訊。 例如，\<xs:element name="e1" /> 會變成 \<xs:element name="e1" type="xs:anyType"/>。 而且，不保留命名空間前置詞。  
  
 如果您指定命名空間參數，產生的結構描述文件將包含該命名空間中所有結構描述元件的定義，即使它們已加入至不同的結構描述文件及 (或) DDL 步驟中也是如此。  
  
 您不能利用這個函數從 **sys.sys** XML 結構描述集合中建構 XML 結構描述文件。  
  
## <a name="examples"></a>範例  
 下列範例會從 `ProductDescriptionSchemaCollection` 資料庫的實際關聯式結構描述中擷取 XML 結構描述集合 `AdventureWorks`。  
  
```  
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [檢視儲存的 XML 結構描述集合](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML 結構描述集合 &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
