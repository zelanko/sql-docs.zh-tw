---
title: TEXTVALID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
caps.latest.revision: 29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: faccfb4456001f6a807e69cc69c89f31e8320955
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982300"
---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>Text 和 Image 函式 - TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  檢查特定文字指標是否為有效的 **text**、**ntext** 或 **image** 函式。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]無法使用替代功能。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>引數  
 *table*  
 這是將使用的資料表名稱。  
  
 *column*  
 這是將使用的資料行名稱。  
  
 *text_ptr*  
 這是將檢查的文字指標。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 如果指標有效，便傳回 1，如果指標無效，便傳回 0。 請注意，**text** 資料行的識別碼必須包含資料表名稱。 如果有效的文字指標不存在，您便無法使用 UPDATETEXT、WRITETEXT 或 READTEXT。  
  
 另外，當您使用 **text**、**ntext** 和 **image** 資料時，下列函式和陳述式也很有用。  
  
|函數或陳述式|Description|  
|---------------------------|-----------------|  
|PATINDEX **(**'*%pattern%**'***,** *expression***)**|傳回指定字元字串在 **text** 和 **ntext** 資料行中的字元位置。|  
|DATALENGTH **(***expression***)**|傳回 **text**、**ntext** 和 **image** 資料行中資料的長度。|  
|SET TEXTSIZE|傳回 SELECT 陳述式所要傳回的 **text**、**ntext** 或 **image** 資料的限制 (以位元組為單位)。|  
  
## <a name="examples"></a>範例  
 下列範例報告 `logo` 資料表之 `pub_info` 資料行中的每個值，是否存在有效的文字指標。  
  
> [!NOTE]  
>  若要執行這個範例，您必須安裝 **pubs** 資料庫。  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Text 和 Image 函式 &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
