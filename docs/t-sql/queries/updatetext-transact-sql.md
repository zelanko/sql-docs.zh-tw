---
title: "UPDATETEXT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 97d10776082f3e4aaa80bfc3f09c662838087518
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新現有**文字**， **ntext**，或**映像**欄位。 若要變更的一部分使用 UPDATETEXT**文字**， **ntext**，或**映像**位置中的資料行。 利用 WRITETEXT 來更新和取代整個**文字**， **ntext**，或**映像**欄位。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用大數值資料類型和**。**WRITE 子句[更新](../../t-sql/queries/update-transact-sql.md)陳述式改為。  
  
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
  
 *table_name* **。** *dest_column_name*  
 這是資料表的名稱和**文字**， **ntext**，或**映像**要更新資料行。 資料表名稱和資料行名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 資料庫名稱和擁有者名稱的指定是選擇性的。  
  
 *dest_text_ptr*  
 文字指標值 （TEXTPTR 函數所傳回） 指向**文字**， **ntext**，或**映像**来更新的資料。 *dest_text_ptr*必須**二進位 (**16**)**。  
  
 *insert_offset*  
 這是以零為基底的更新起始位置。 如**文字**或**映像**資料行， *insert_offset*是插入新資料之前略過從現有的資料行開頭的位元組數。 如**ntext**資料行， *insert_offset*是字元數目 (每個**ntext**字元使用 2 個位元組)。 現有**文字**， **ntext**，或**映像**這個以零為起始的起始位置開始的資料會移往右移以騰出空間給新的資料。 0 值會將新資料插入現有資料的起點。 NULL 值會將新資料附加至現有的資料值。  
  
 *delete_length*  
 這是要刪除從現有的資料長度**文字**， **ntext**，或**映像**資料行中，開始*insert_offset*位置。 *Delete_length*以位元組為單位的指定值**文字**和**映像**資料行和字元**ntext**資料行。 每個**ntext**字元使用 2 個位元組。 0 值不會刪除任何資料。 NULL 值會刪除所有的資料，從*insert_offset*位置到末端的現有**文字**或**映像**資料行。  
  
 WITH LOG  
 記錄取決於資料庫的實際復原模式。  
  
 *inserted_data*  
 要插入至現有的資料**文字**， **ntext**，或**映像**資料行在*insert_offset*位置。 這是單一**char**， **nchar**， **varchar**， **nvarchar**，**二進位**， **varbinary**，**文字**， **ntext**，或**映像**值。 *inserted_data*可以是常值或變數。  
  
 *table_name.src_column_name*  
 這是資料表的名稱和**文字**， **ntext**，或**映像**做為插入的資料來源的資料行。 資料表名稱和資料行名稱必須符合識別碼的規則。  
  
 *src_text_ptr*  
 文字指標值 （TEXTPTR 函數所傳回） 指向**文字**， **ntext**，或**映像**做為插入的資料來源的資料行。  
  
> [!NOTE]  
>  *scr_text_ptr*值不能與相同*dest_text_ptr*值。  
  
## <a name="remarks"></a>備註  
 新插入的資料可以是單一*inserted_data*常數、 資料表名稱、 資料行名稱或文字指標。  
  
|更新動作|UPDATETEXT 參數|  
|-------------------|---------------------------|  
|若要取代現有的資料|指定非 null *insert_offset*值、 非零*delete_length*值，以及要插入新的資料。|  
|若要刪除現有的資料|指定非 null *insert_offset*值和非零*delete_length*。 請勿指定要插入的新資料。|  
|若要插入新的資料|指定*insert_offset*值*delete_length*為 0，且要插入新的資料。|  
  
 我們建議，為了達到最佳效能**文字**， **ntext**和**映像**插入或更新的區塊大小會以 8,040 位元組倍數的資料。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，同資料列文字指標**文字**， **ntext**，或**映像**資料可能存在而無效。 Text in row 選項的相關資訊，請參閱[sp_tableoption &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 如需讓文字指標無效的資訊，請參閱[sp_invalidate_textptr &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 初始化**文字**資料行設為 NULL，請使用 WRITETEXT;UPDATETEXT 初始化**文字**資料行設為空字串。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [READTEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40;TRANSACT-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
