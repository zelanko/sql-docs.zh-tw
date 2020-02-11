---
title: sys.syscomments （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 183fa2fc1a674ec1cc987c265f5a0d4c399e27cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68010754"
---
# <a name="syssyscomments-transact-sql"></a>sys.syscomments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含資料庫中每份檢視、規則、預設值、觸發程序、CHECK 條件約束、DEFAULT 條件約束以及預存程序的項目。 **Text**資料行包含原始 SQL 定義語句。  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]我們建議您改用 sys.sql_modules。 如需詳細資訊，請參閱[sql_modules &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**號**|**int**|這個文字所套用的物件識別碼。|  
|**number**|**smallint**|程序分組中的數字 (如果有分組的話)。<br /><br /> 0 = 項目不是程序。|  
|**colid**|**smallint**|超過 4,000 個字元的物件定義資料列序號。|  
|**狀態**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**ctext**|**Varbinary （8000）**|SQL 定義陳述式的原始位元組。|  
|**texttype**|**smallint**|0 = 使用者提供的註解<br /><br /> 1 = 系統提供的註解<br /><br /> 4 = 加密的註解|  
|**語言**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**加密**|**bit**|指出程序定義是否會模糊化。<br /><br /> 0 = 不模糊化<br /><br /> 1 = 模糊化<br /><br /> ** \* \*重要\*事項**若要模糊處理預存程序定義，請使用 CREATE PROCEDURE 搭配 ENCRYPTION 關鍵字。|  
|**壓縮**|**bit**|永遠傳回 0。 這表示程序已經壓縮。|  
|**text**|**nvarchar(4000)**|SQL 定義陳述式的實際文字。<br /><br /> 已解碼運算式的語意相當於原始文字，但是不能保證語法相同。 例如，空白字元會從已解碼的運算式移除。<br /><br /> 這個[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]相容的視圖會從目前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的結構取得資訊，並傳回比**Nvarchar （4000）** 定義更多的字元。 **sp_help**會傳回**Nvarchar （4000）** 做為文字資料行的資料類型。 使用**sys.syscomments**時，請考慮使用**Nvarchar （max）**。 針對新的開發工作，請勿使用**sys.syscomments**。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的相容性檢視](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
