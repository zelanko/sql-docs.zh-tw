---
title: 架構（Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 16b2a23c696b4da405e4983689217abb15074f03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078436"
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對目前資料庫中每個結構描述，各傳回一個資料列。 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。 若要取出實例中所有資料庫的相關資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請[&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視中查詢 sys.databases。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|目前資料庫的名稱|  
|**SCHEMA_NAME**|**Nvarchar （** 128 **）**|傳回結構描述的名稱。|  
|**SCHEMA_OWNER**|**Nvarchar （** 128 **）**|結構描述擁有者名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**Varchar （** 6 **）**|一律傳回 NULL。|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**Varchar （** 3 **）**|一律傳回 NULL。|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|傳回預設字元集的名稱。|  

**範例**  
下列範例會傳回 master 資料庫中之架構的相關資訊：  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊架構視圖 &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [syscharsets &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
