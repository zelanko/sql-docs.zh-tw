---
description: sp_helplanguage (Transact-SQL)
title: sp_helplanguage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 72f2e867c8139045b107cbb99871742c26440ee4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489324"
---
# <a name="sp_helplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  報告特定替代語言或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中所有語言的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @language = ] 'language'` 這是要顯示資訊的替代語言名稱。 *language* 是 **sysname**，預設值是 Null。 如果指定 *語言* ，則會傳回指定之語言的相關資訊。 如果未指定語言，則會傳回 **sys.sys語言** 相容性檢視中所有語言的相關資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|語言識別碼。|  
|**dateformat**|**nchar(3)**|日期的格式。|  
|**datefirst**|**tinyint**|每週第一天：1 代表星期一，2 代表星期二，依此類推，7 則代表星期日。|  
|**升級**|**int**|這個語言最後升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|**name**|**sysname**|語言名稱。|  
|**alias**|**sysname**|語言的替代名稱。|  
|**months**|**nvarchar(372)**|月份名稱。|  
|**shortmonths**|**nvarchar(132)**|簡短月份名稱。|  
|**天**|**nvarchar(217)**|日期名稱。|  
|**lcid**|**int**|語言的 Windows 地區設定識別碼。|  
|**msglangid**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訊息群組識別碼。|  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-information-about-a-single-language"></a>A. 傳回單一語言的相關資訊  
 下列範例會顯示替代語言 `French` 的相關資訊。  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. 傳回所有語言的相關資訊  
 下列範例會顯示所有已安裝之替代語言的相關資訊。  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE &#40;Transact-sql&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
