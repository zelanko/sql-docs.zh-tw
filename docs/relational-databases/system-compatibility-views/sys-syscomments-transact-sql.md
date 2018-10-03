---
title: sys.syscomments (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscomments_TSQL
- syscomments
- syscomments_TSQL
- sys.syscomments
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscomments compatibility view
- syscomments system table
ms.assetid: 767dd410-6bc9-4c4a-ab0f-6d2cf6163426
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 12d6c57e59ee37443b9ec600d8eb760c7f53018a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843776"
---
# <a name="syssyscomments-transact-sql"></a>sys.syscomments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含資料庫中每份檢視、規則、預設值、觸發程序、CHECK 條件約束、DEFAULT 條件約束以及預存程序的項目。 **文字**資料行包含原始的 SQL 定義陳述式。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]我們建議您改用 sys.sql_modules。 如需詳細資訊，請參閱 < [sys.sql_modules &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|這個文字所套用的物件識別碼。|  
|**number**|**smallint**|程序分組中的數字 (如果有分組的話)。<br /><br /> 0 = 項目不是程序。|  
|**colid**|**smallint**|超過 4,000 個字元的物件定義資料列序號。|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**ctext**|**varbinary(8000)**|SQL 定義陳述式的原始位元組。|  
|**texttype**|**smallint**|0 = 使用者提供的註解<br /><br /> 1 = 系統提供的註解<br /><br /> 4 = 加密的註解|  
|**語言**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**加密**|**bit**|指出程序定義是否會模糊化。<br /><br /> 0 = 不模糊化<br /><br /> 1 = 模糊化<br /><br /> **\*\* 重要\* \*** 来模糊化預存程序定義，請使用 CREATE PROCEDURE 搭配 ENCRYPTION 關鍵字。|  
|**compressed**|**bit**|永遠傳回 0。 這表示程序已經壓縮。|  
|**text**|**nvarchar(4000)**|SQL 定義陳述式的實際文字。<br /><br /> 已解碼運算式的語意相當於原始文字，但是不能保證語法相同。 例如，空白字元會從已解碼的運算式移除。<br /><br /> 這[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-相容檢視會取得從目前的資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構，並可傳回字元數會多於**nvarchar(4000)** 定義。 **sp_help**會傳回**nvarchar(4000)** 做為文字資料行資料類型。 使用時**ctext**建議您使用**nvarchar （max)**。 新的開發工作，請勿使用**ctext**。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
