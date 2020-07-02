---
title: VIEWS （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1a910110ac34ebcd52dacf2c4f549f76f44cb06
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85647265"
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  針對目前資料庫中目前使用者所能存取的，傳回一個資料列。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**Nvarchar （** 128 **）**|檢視限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar （** 128 **）**|包含檢視的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 只有可靠的方法可以尋找物件的架構，就是查詢 sys.databases 目錄檢視。|  
|**TABLE_NAME**|**Nvarchar （** 128 **）**|檢視名稱。|  
|**VIEW_DEFINITION**|**Nvarchar （** 4000 **）**|如果定義的長度大於**Nvarchar （** 4000 **）**，這個資料行就是 Null。 否則，這個資料行就是檢視定義文字。|  
|**CHECK_OPTION**|**Varchar （** 7 **）**|WITH CHECK OPTION 的類型。 如果原始檢視是利用 WITH CHECK OPTION 所建立，則為 CASCADE。 否則，就傳回 NONE。|  
|**IS_UPDATABLE**|**Varchar （** 2 **）**|指定檢視是否可以更新。 一律傳回 NO。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊架構視圖 &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
