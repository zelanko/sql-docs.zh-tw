---
title: UPDATETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf01a97b6337f154de8d6d8e2c0fb71f7c4a1dd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33065495"
---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新現有的 **text**、**ntext** 或 **image** 欄位。 請使用 UPDATETEXT 來適當地只變更 **text**、**ntext** 或 **image** 資料行中的一部分。 使用 WRITETEXT 來更新和取代整個 **text**、**ntext** 或 **image** 欄位。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用大數值資料類型和 [UPDATE](../../t-sql/queries/update-transact-sql.md) 陳述式的 **.** WRITE 子句。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATETEXT [BULK] { table_name.dest_column_name dest_text_ptr }  
  { NULL | insert_offset }  
     { NULL | delete_length }  
     [ WITH LOG ]  
     [ inserted_data  
    | { table_name.src_column_name src_text_ptr } ]  
```  
  
## <a name="arguments"></a>引數  
 BULK  
 讓上傳工具能夠上傳二進位資料流。 此資料流必須由位於 TDS 通訊協定層級的工具提供。 當資料流不存在時，查詢處理器就會忽略 BULK 選項。  
  
> [!IMPORTANT]  
>  我們建議您不要將 BULK 選項用於以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為基礎的應用程式中。 未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本可能會變更或移除這個選項。  
  
 *table_name* **.** *dest_column_name*  
 這是要更新之資料表及 **text**、**ntext** 或 **image** 資料行的名稱。 資料表名稱和資料行名稱必須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。 資料庫名稱和擁有者名稱的指定是選擇性的。  
  
 *dest_text_ptr*  
 這是指向要更新之 **text**、**ntext** 或 **image** 資料的文字指標值 (TEXTPTR 函數所傳回)。 *dest_text_ptr* 必須是 **binary(** 16 **)**。  
  
 *insert_offset*  
 這是以零為基底的更新起始位置。 就 **text** 或 **image** 資料行而言，*insert_offset* 是在插入新資料之前，要從現有資料行開頭略過的位元組數。 就 **ntext** 資料行而言，*insert_offset* 則是字元數目 (每個 **ntext** 字元會使用 2 個位元組)。 從這個以零為基底之起始位置開始的現有 **text**、**ntext** 或 **image** 資料，會向右移來騰出空間供新資料使用。 0 值會將新資料插入現有資料的起點。 NULL 值會將新資料附加至現有的資料值。  
  
 *delete_length*  
 這是要從現有 **text**、**ntext** 或 **image** 資料行中刪除的資料長度，從 *insert_offset*位置開始。 指定 *delete_length* 值時，針對 **text** 和 **image** 資料行，會以位元組為單位來指定，針對 **ntext** 資料行，則以字元為單位來指定。 每個 **ntext** 字元都使用 2 個位元組。 0 值不會刪除任何資料。 值為 NULL 時，會刪除從 *insert_offset* 位置到現有 **text** 或 **image** 資料行結尾的所有資料。  
  
 WITH LOG  
 記錄取決於資料庫的實際復原模式。  
  
 *inserted_data*  
 這是要在現有 **text**、**ntext** 或 **image** 資料行的 *insert_offset* 位置插入的資料。 這是單一的 **char**、**nchar**、**varchar**、**nvarchar**、**binary**、**varbinary**、**text**、**ntext** 或 **image** 值。 *inserted_data* 可以是常值或變數。  
  
 *table_name.src_column_name*  
 這是用來作為所插入資料之來源的資料表及 **text**、**ntext** 或 **image** 資料行的名稱。 資料表名稱和資料行名稱必須符合識別碼的規則。  
  
 *src_text_ptr*  
 這是指向用來作為所插入資料之來源的 **text**、**ntext** 或 **image** 資料行的文字指標值 (TEXTPTR 函數所傳回)。  
  
> [!NOTE]  
>  *scr_text_ptr* 值不得與 *dest_text_ptr* 值相同。  
  
## <a name="remarks"></a>Remarks  
 新插入的資料可以是單一 *inserted_data* 常數、資料表名稱、資料行名稱或文字指標。  
  
|更新動作|UPDATETEXT 參數|  
|-------------------|---------------------------|  
|若要取代現有的資料|請指定非 Null 的 *insert_offset* 值、非零的 *delete_length* 值，以及要插入的新資料。|  
|若要刪除現有的資料|請指定非 Null *insert_offset* 值和非零的 *delete_length*。 請勿指定要插入的新資料。|  
|若要插入新的資料|請指定 *insert_offset* 值、值為 0 的 *delete_length* ，以及要插入的新資料。|  
  
 為了獲得最佳效能，建議您以 8,040 個位元組之倍數的片段大小來插入或更新 **text**、**ntext** 及 **image** 資料。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，可能有指向 **text**、**ntext** 或 **image** 資料的同資料列文字指標存在，但可能無效。 如需有關 text in row 選項的資訊，請參閱[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)。 如需有關讓文字指標變成無效的資訊，請參閱 [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)。  
  
 若要將 **text** 資料行初始化為 NULL，請使用 WRITETEXT；UPDATETEXT 會將 **text** 資料行初始化為空字串。  
  
## <a name="permissions"></a>Permissions  
 需要指定之資料表的 UPDATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例將文字指標放在區域變數 `@ptrval` 中，再利用 `UPDATETEXT` 來更新拼字錯誤。  
  
> [!NOTE]  
>  若要執行這個範例，您必須安裝 pubs 資料庫。  
  
```  
USE pubs;  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
DECLARE @ptrval binary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr, publishers p  
      WHERE p.pub_id = pr.pub_id   
      AND p.pub_name = 'New Moon Books'  
UPDATETEXT pub_info.pr_info @ptrval 88 1 'b';  
GO  
ALTER DATABASE pubs SET RECOVERY FULL;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
