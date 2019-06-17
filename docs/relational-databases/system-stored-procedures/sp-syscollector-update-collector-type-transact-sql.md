---
title: sp_syscollector_update_collector_type (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collector_type_TSQL
- sp_syscollector_update_collector_type
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 3c414dfd-d9ca-4320-81aa-949465b967bf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d3529d01966c7f9780183d663823d8f4033f47a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63001354"
---
# <a name="spsyscollectorupdatecollectortype-transact-sql"></a>sp_syscollector_update_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新收集項的收集器型別。 指定收集器型別的名稱和 GUID 之後，就會更新收集器型別組態，包括收集和上傳封裝、參數結構描述，以及參數格式器結構描述。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_update_collector_type [ @collector_type_uid = ] 'collector_type_uid' OUTPUT  
          , [ @name = ] 'name'  
          , [ @parameter_schema = ] 'parameter_schema'  
          , [ @collection_package_id = ] collection_package_id  
          , [ @upload_package_id = ] upload_package_id  
```  
  
## <a name="arguments"></a>引數  
`[ @collector_type_uid = ] 'collector_type_uid'` 是收集器型別的 GUID。 *collector_type_uid 是否*已**uniqueidentifier**，而且如果它是的 NULL，它會自動建立並當做 OUTPUT 傳回。  
  
`[ @name = ] 'name'` 是收集器型別的名稱。 *名稱*已**sysname**必須加以指定。  
  
`[ @parameter_schema = ] 'parameter_schema'` 是此收集器類型的 XML 結構描述。 *parameter_schema*已**xml** ，且可能會需要特定收集器類型。 如果它不是必要項目，這個引數就可能是 NULL。  
  
`[ @collection_package_id = ] collection_package_id` 指向的本機唯一識別碼[!INCLUDE[ssIS](../../includes/ssis-md.md)]收集組所使用的收集封裝。 *collection_package_id*已**uniqueidentifier** ，且需要。 若要取得的值*collection_package_id*，查詢 msdb 資料庫中的 dbo.syscollector_collector_types 系統檢視。  
  
`[ @upload_package_id = ] upload_package_id` 指向的本機唯一識別碼[!INCLUDE[ssIS](../../includes/ssis-md.md)]上傳收集組所使用的封裝。 *upload_package_id*已**uniqueidentifier** ，且需要。 若要取得的值*upload_package_id*，查詢 msdb 資料庫中的 dbo.syscollector_collector_types 系統檢視。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**dc_admin** （具有 EXECUTE 權限） 固定的資料庫角色。  
  
## <a name="example"></a>範例  
 此範例會更新一般 T-SQL 查詢收集器型別 (在此範例中，將會使用一般 T-SQL 查詢收集器型別的預設結構描述)。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collector_type  
@collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
  <xs:element name="TSQLQueryCollector">  
<xs:complexType>  
  <xs:sequence>  
<xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Value" type="xs:string" />  
  <xs:element name="OutputTable" type="xs:string" />  
</xs:sequence>  
  </xs:complexType>  
</xs:element>  
<xs:element name="Databases" minOccurs="0" maxOccurs="1">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
</xs:sequence>  
<xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
<xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
  </xs:complexType>  
</xs:element>  
  </xs:sequence>  
</xs:complexType>  
  </xs:element>  
</xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
