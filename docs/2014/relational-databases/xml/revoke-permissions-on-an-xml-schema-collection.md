---
title: 撤銷 XML 結構描述集合上的權限 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- revoking permissions [SQL Server]
ms.assetid: 4e542b70-2d56-4a65-8a39-96a1ed477ca6
author: rothja
ms.author: jroth
ms.openlocfilehash: 247364d01575e9ffae5988df03c82ea198289507
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065438"
---
# <a name="revoke-permissions-on-an-xml-schema-collection"></a>撤銷 XML 結構描述集合上的權限
  建立 XML 結構描述集合的權限可以使用下列其中一種方式來撤銷：  
  
-   撤銷關聯式結構描述的 ALTER 權限。 然後，主體便無法在關聯式結構描述中建立 XML 結構描述集合。 但是，主體仍然可以在同一資料庫的其他關聯式結構描述中建立 XML 結構描述集合。  
  
-   撤銷資料庫上主體的 ALTER ANY SCHEMA 權限。 然後，主體便無法在資料庫中的任何位置建立 XML 結構描述集合。  
  
-   撤銷資料庫上主體的 CREATE XML SCHEMA COLLECTION 或 ALTER XML SCHEMA COLLECTION 權限。 這樣可以防止主體於資料庫中匯入 XML 結構描述集合。 撤銷資料庫上的 ALTER 或 CONTROL 權限也有相同的效果。  
  
## <a name="revoking-permissions-on-an-existing-xml-schema-collection-object"></a>撤銷現有 XML 結構描述集合物件上的權限  
 下列為可以在 XML 結構描述集合上撤銷的權限，以及其結果：  
  
-   撤銷 ALTER 權限會讓主體無法修改 XML 結構描述集合的內容。  
  
-   撤銷 TAKE OWNERSHIP 權限會讓主體無法轉移 XML 結構描述集合的擁有權。  
  
-   撤銷 REFERENCES 權限會讓主體無法使用 XML 結構描述集合設定 xml 類型的資料行和參數類型，或約束 xml 類型的資料行和參數 (資料行限於資料表和檢視)。 這樣也會撤銷從其他 XML 結構描述集合參考此結構描述集合的權限。  
  
-   撤銷 VIEW DEFINITION 權限會讓主體無法檢視 XML 結構描述集合的內容。  
  
-   撤銷 EXECUTE 權限會讓主體無法插入或更新具類型或受 XML 集合所約束之資料行、變數和參數中的值。 這樣也撤銷了查詢這種 **xml** 類型之資料行、變數或參數的能力。  
  
## <a name="examples"></a>範例  
 下列範例中的狀況說明 XML 結構描述權限如何運作。 每個範例都會建立所需的測試資料庫、關聯式結構描述和登入。 將會授與這些登入必要的 XML 結構描述集合權限。 每個範例都會在結束時執行必要的清除。  
  
### <a name="a-revoking-permissions-to-create-an-xml-schema-collection"></a>A. 撤銷可建立 XML 結構描述集合的權限  
 這個範例將建立登入和範例資料庫， 並在資料庫中加入關聯式結構描述。 首先，登入會被授與兩個關聯式結構描述上的 ALTER 權限，以及其他建立 XML 結構描述集合的必要權限。 然後，此範例會撤銷資料庫中其中一個關聯式結構描述上的 ALTER 權限。 這樣登入就無法建立 XML 結構描述集合。  
  
```  
setuser  
go  
create login TestLogin1 with password='SQLSvrPwd1'  
go  
create database SampleDBForSchemaPermissions  
go  
use SampleDBForSchemaPermissions  
go  
-- Create another relational schema in the db (in addition to dbo schema)  
CREATE SCHEMA myOtherDBSchema  
go  
CREATE USER TestLogin1  
go  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed  
-- CREATE XML SCHEMA is a database level permission  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
go  
-- Now TestLogin1 can import an XML schema collection in both relational schemas.  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- TestLogin1 can create XML schema collection in myOtherDBSchema relational schema  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- Let us drop XML schema collections from both relational schemas  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
go  
DROP XML SCHEMA COLLECTION dbo.myTestSchemaCollection  
go  
-- now REVOKE permission from TestLogin1 to alter myOtherDBSchema  
setuser  
go  
REVOKE ALTER ON SCHEMA::myOtherDBSchema FROM TestLogin1  
go  
-- now TestLogin1 cannot create xml schema collection in myOtherDBSchema  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- TestLogin1 can still create XML schema collections in dbo  
-- It cannot create XML schema collections anywhere in the database  
-- if we REVOKE CREATE XML SCHEMA COLLECTION permission  
SETUSER  
go  
REVOKE CREATE XML SCHEMA COLLECTION FROM TestLogin1  
go  
  
setuser 'TestLogin1'  
go  
-- the following now should fail  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- Final cleanup  
SETUSER  
go  
USE master  
go  
DROP DATABASE SampleDBForSchemaPermissions  
go  
DROP LOGIN TestLogin1  
Go  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](xml-data-sql-server.md)   
 [比較具類型的 XML 與不具類型的 XML](compare-typed-xml-to-untyped-xml.md)   
 [XML 結構描述集合 &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)   
 [伺服器上 XML 結構描述集合的需求與限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
