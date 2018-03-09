---
title: "sp_helplanguage (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a94f66688ce53aef2dcf575d58e16ed6f2f1672b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  報告特定替代語言或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中所有語言的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@language=** ] **'***語言***'**  
 這是要顯示資訊的替代語言名稱。 *語言*是**sysname**，預設值是 NULL。 如果*語言*已指定，會傳回指定語言的相關資訊。 如果未指定語言，在 所有語言的相關資訊**sys.syslanguages**相容性檢視會傳回。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|語言識別碼。|  
|**dateformat**|**nchar(3)**|日期的格式。|  
|**datefirst**|**tinyint**|每週第一天：1 代表星期一，2 代表星期二，依此類推，7 則代表星期日。|  
|**升級**|**int**|這個語言最後升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。|  
|**name**|**sysname**|語言名稱。|  
|**別名**|**sysname**|語言的替代名稱。|  
|**幾個月**|**nvarchar(372)**|月份名稱。|  
|**shortmonths**|**nvarchar(132)**|簡短月份名稱。|  
|**天**|**nvarchar(217)**|日期名稱。|  
|**lcid**|**int**|語言的 Windows 地區設定識別碼。|  
|**msglangid**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訊息群組識別碼。|  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>請參閱  
 [Database Engine 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [設定語言 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
