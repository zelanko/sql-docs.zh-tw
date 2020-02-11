---
title: sp_syscollector_create_collector_type （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collector_type
- sp_syscollector_create_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 568e9119-b9b0-4284-9cef-3878c691de5f
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd8c82a401f78f4907bb891ede845017c00ac5ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68032630"
---
# <a name="sp_syscollector_create_collector_type-transact-sql"></a>sp_syscollector_create_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立資料收集器的收集器型別。 收集器型別是[!INCLUDE[ssIS](../../includes/ssis-md.md)]封裝周圍的邏輯包裝函式，可提供實際機制來收集資料，並將它上傳到管理資料倉儲。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_create_collector_type   
    [ [@collector_type_uid = ] 'collector_type_uid' OUTPUT ]  
    , [ @name = ] 'name'  
    , [ [ @parameter_schema = ] 'parameter_schema' ]  
    , [ [ @parameter_formatter = ] 'parameter_formatter' ]  
    , [ @collection_package_id = ] 'collection_package_id'  
    , [ @upload_package_id = ] 'upload_package_id'  
```  
  
## <a name="arguments"></a>引數  
 [ @collector_type_uid = ]'*collector_type_uid*'  
 這是收集器類型的 GUID。 *collector_type_uid*是**uniqueidentifier** ，而且如果是 Null，則會自動建立並當做輸出傳回。  
  
 [ @name = ]'*name*'  
 這是收集器類型的名稱。 *名稱*是**sysname** ，必須指定。  
  
 [ @parameter_schema = ]'*parameter_schema*'  
 這是此收集器類型的 XML 結構描述。 *parameter_schema*是**xml** ，預設值是 Null。  
  
 [ @parameter_formatter = ]'*parameter_formatter*'  
 這是用來轉換 XML，以用於收集組屬性頁中的範本。 *parameter_formatter*是**xml** ，預設值是 Null。  
  
 [@collection_package_id = ]*collection_package_id*  
 這是指向收集組所使用之 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 收集封裝的本機唯一識別碼。 *collection_package_id*是**uniqueidentifier** ，而且是必要的。  
  
 [@upload_package_id = ]*upload_package_id*  
 這是指向收集組所使用之 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 上傳封裝的本機唯一識別碼。 *upload_package_id*是**uniqueidentifier** ，而且是必要的。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="permissions"></a>權限  
 需要 dc_admin (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="example"></a>範例  
 這會建立一般 T-SQL 查詢收集器型別。  
  
```  
EXEC sp_syscollector_create_collector_type  
@collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419',  
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
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
