---
description: VIEWS (Transact-SQL)
title: VIEWS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs:
- TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0a5656cac26865f58549e6531e371970b8afe205
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753540"
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  針對目前資料庫中目前使用者所能存取的，傳回一個資料列。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**Nvarchar (** 128 **) **|檢視限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar (** 128 **) **|包含檢視的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;**  只有可靠的方法可尋找物件的架構，就是查詢 sys. objects 目錄檢視。|  
|**TABLE_NAME**|**Nvarchar (** 128 **) **|檢視名稱。|  
|**VIEW_DEFINITION**|**Nvarchar (** 4000 **) **|如果定義的長度大於 **Nvarchar (** 4000 **) **，這個資料行就是 Null。 否則，這個資料行就是檢視定義文字。|  
|**CHECK_OPTION**|**Varchar (** 7 **) **|WITH CHECK OPTION 的類型。 如果原始檢視是利用 WITH CHECK OPTION 所建立，則為 CASCADE。 否則，就傳回 NONE。|  
|**IS_UPDATABLE**|**Varchar (** 2 **) **|指定檢視是否可以更新。 一律傳回 NO。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](../../t-sql/language-reference.md)   
 [&#40;Transact-sql&#41;的資訊架構視圖 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
