---
title: 拒絕 XML 結構描述集合的權限 | Microsoft 文件
description: 了解如何拒絕建立新 XML 結構描述集合或使用現有結構描述集合的權限。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- denying permissions [SQL Server], XML server collections
ms.assetid: e2b300b0-e734-4c43-a4da-c78e6e5d4fba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4084b87320da45e4cff3aa37ba852f708da8976c
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388483"
---
# <a name="deny-permissions-on-an-xml-schema-collection"></a>拒絕 XML 結構描述集合的權限
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  可以拒絕建立新 XML 結構描述集合或使用現有結構描述集合的權限。  
  
## <a name="denying-permission-to-create-an-xml-schema-collection"></a>對於建立 XML 結構描述集合的拒絕權限  
 您可以用下列方式來拒絕建立 XML 結構描述集合的權限：  
  
-   拒絕對關聯式結構描述的 ALTER 權限。  
  
-   拒絕對關聯式結構描述的 CONTROL，以拒絕對於關聯式結構描述以及所有包含物件的所有權限。  
  
-   拒絕對資料庫的 ALTER ANY SCHEMA。 在此情況下，主體將無法在資料庫中的任何位置建立 XML 結構描述集合。 請注意拒絕資料庫的 ALTER 或 CONTROL 權限，將會拒絕資料庫中所有物件的所有權限。  
  
## <a name="denying-permissions-on-an-xml-schema-collection-object"></a>XML 結構描述集合物件的拒絕權限  
 以下是可拒絕現有 XML 結構描述集合與結果的權限：  
  
-   拒絕 ALTER 權限可拒絕主體修改 XML 結構描述集合的內容。  
  
-   拒絕 CONTROL 權限可拒絕主體執行 XML 結構描述集合的任何作業。  
  
-   拒絕 REFERENCES 權限可拒絕主體使用結構描述集合，來約束 xml 類型資料行與參數或設定其類型。 它也會拒絕主體從其他 XML 結構描述集合參考此 XML 結構描述集合。  
  
-   拒絕 VIEW DEFINITION 權限可拒絕主體檢視 XML 結構描述集合的內容。  
  
-   拒絕 EXECUTE 權限可拒絕主體在 XML 結構描述集合所約束或設定其類型的資料行、變數及參數中插入或更新值。 它也會拒絕主體在相同的 xml 類型資料行與變數中查詢值。  
  
## <a name="examples"></a>範例  
 下列範例中的狀況顯示 XML 結構描述權限的運作方式。 每個範例都會建立所需的測試資料庫、關聯式結構描述和登入。 將會授與這些登入必要的 XML 結構描述集合權限。 每個範例都會在結束時執行必要的清除。  
  
### <a name="a-preventing-a-user-from-creating-an-xml-schema-collection"></a>A. 防止使用者建立 XML 結構描述集合  
 有一個方法可防止使用者建立 XML 結構描述集合，就是拒絕對關聯式結構描述的 ALTER 權限。 下列範例會顯示這一點。  
  
 本範例會建立使用者 `TestLogin1`和資料庫。 除了 `dbo` 結構描述之外，它也在資料庫中建立關聯式結構描述。 一開始， `CREATE XML SCHEMA` 權限允許使用者在資料庫中的任何位置建立結構描述集合。 此範例接著會在其中一個關聯式結構描述上，拒絕使用者的 `ALTER` 權限。 這將可防止使用者在該關聯式結構描述中建立 XML 結構描述集合。  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
GO  
-- Now deny permission from TestLogin1 to alter myOtherDBSchema.  
setuser  
GO  
DENY ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
GO  
-- Now TestLogin1 cannot create xml schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="b-denying-permissions-on-an-xml-schema-collection"></a>B. XML 結構描述集合的拒絕權限  
 下列範例顯示如何針對某個登入來拒絕現有 XML 結構描述集合上的特定權限。 在此範例中，對某個測試登入拒絕現有 XML 結構描述集合的 REFERENCES 權限。  
  
 本範例會建立使用者 `TestLogin1`和資料庫。 除了 `dbo` 結構描述之外，它也在資料庫中建立關聯式結構描述。 一開始， `CREATE XML SCHEMA` 權限允許使用者在資料庫中的任何位置建立結構描述集合。  
  
 XML 結構描述集合上的 `REFERENCES` 權限能讓 `TestLogin1` 在資料表中建立具類型的 `xml` 資料行時使用結構描述。 如果拒絕 XML 結構描述集合上的 `REFERENCES` 權限，會使得 `TestLogin1` 無法使用 XML 結構描述集合。  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, the following  
-- permission is required.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant permission to TestLogin1 to create a table and reference the XML schema collection.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also needs REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on the schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection   
TO TestLogin1  
GO  
  
--TestLogin1 can use the schema.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
-- Drop the table.  
DROP TABLE T  
GO  
-- Now deny REFERENCES permission to TestLogin1 on the schema created previously.  
SETUSER  
GO  
DENY REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection TO TestLogin1  
  
GO  
-- Now TestLogin1 cannot create xml schema collection  
SETUSER 'TestLogin1'  
GO  
-- Following statement fails. TestLogin1 does not have REFERENCES   
-- permission on the XML schema collection.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 結構描述集合 &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [伺服器上 XML 結構描述集合的需求與限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)   
 [DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
