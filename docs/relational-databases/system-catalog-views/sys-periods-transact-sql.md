---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
author: stevestein
ms.author: sstein
ms.openlocfilehash: eea7709c67eab0dc9fe1890135f9ae03225cdff2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68068087"
---
# <a name="sysperiods-transact-sql"></a>sys.databases （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對已定義週期的每個資料表，各傳回一個資料列。  
  
|資料行標頭|資料類型|描述|  
|-------------------|---------------|-----------------|  
|NAME|**sysname**|期間的名稱|  
|period_type|**tinyint**|代表期間類型的數值：<br /><br /> 1 = 系統時間週期|  
|period_type_desc|**nvarchar(60)**|資料行類型的文字描述：<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|包含 period_type 資料行之資料表的識別碼|  
|start_column_id|**int**|定義較低 period 界限的資料行識別碼|  
|end_column_id|**int**|定義上限時間界限的資料行識別碼|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [system_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [時態表](../../relational-databases/tables/temporal-tables.md)  
  
  
