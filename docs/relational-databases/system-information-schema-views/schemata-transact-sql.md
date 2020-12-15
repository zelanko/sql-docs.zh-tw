---
description: SCHEMATA (Transact-SQL)
title: 架構 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 847e046c89a11ec8d26db47d33f6f605c24cef28
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474709"
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  針對目前資料庫中每個結構描述，各傳回一個資料列。 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。 若要取得實例中所有資料庫的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請查詢 [sys. 資料庫 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|目前資料庫的名稱|  
|**SCHEMA_NAME**|**Nvarchar (** 128 **)**|傳回結構描述的名稱。|  
|**SCHEMA_OWNER**|**Nvarchar (** 128 **)**|結構描述擁有者名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 INFORMATION_SCHEMA views 只代表物件的中繼資料子集。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**Varchar (** 6 **)**|一律傳回 NULL。|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**Varchar (** 3 **)**|一律傳回 NULL。|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|傳回預設字元集的名稱。|  

**範例**  
下列範例會傳回 master 資料庫中架構的相關資訊：  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](../../t-sql/language-reference.md)   
 [&#40;Transact-sql&#41;的資訊架構視圖 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.sys字元集 &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
