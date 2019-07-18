---
title: READTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- READTEXT_TSQL
- READTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- column reading [SQL Server]
- READTEXT statement
- reading columns
ms.assetid: 91b69853-1381-4306-8343-afdb73105738
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: f2c07b756c608e5e28de3351d887d7a7b2f051ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62927585"
---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

從 **text**、**ntext** 或 **image** 資料行中讀取 **text**、**ntext** 或 **image** 值。 從所指定位移開始讀取指定數目的位元組。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [SUBSTRING](../../t-sql/functions/substring-transact-sql.md) 函數。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>引數  
_table_ **.** _column_  
這是要讀取的資料表和資料行名稱。 資料表和資料行名稱必須滿足[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。 您必須指定資料表和資料行名稱；不過，資料庫名稱和擁有者名稱的指定是選擇性的。  
  
_text\_ptr_  
這是一個有效的文字指標。 _text\_ptr_ 必須是 **binary(16)** 。  
  
_offset_  
是使用 **text** 或 **image** 資料類型時的位元組數目。 它也可以是開始讀取 **text**、**image** 或 **ntext** 資料之前，**ntext** 資料類型用來略過的字元位元組數目。  
  
_size_ 是使用 **text** 或 **image** 資料類型時的位元組數目。 它也可以是 **ntext** 資料類型用於資料讀取時的字元位元組數目。 如果 _size_ 是 0，就會讀取 4 KB 位元組的資料。  
  
HOLDLOCK  
造成讀取文字值的鎖定，直到交易結束為止。 其他使用者可以讀取值，但無法加以修改。  
  
## <a name="remarks"></a>Remarks  
請使用 [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) 函式來取得有效的 _text\_ptr_ 值。 TEXTPTR 會傳回指定資料列中 **text**、**ntext** 或 **image** 資料行的指標。 如果查詢傳回多個資料列，TEXTPRT 也可以傳回指向查詢所傳回最後一個資料列之 **text**、**ntext** 或 **image** 資料行的指標。 由於 TEXTPTR 會傳回 16 位元組二進位字串，我們建議您宣告一個本機變數來存放文字指標，再搭配 READTEXT 來使用這個變數。 如需有關宣告本機變數的詳細資訊，請參閱 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)。  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，同資料列文字指標有可能存在而無效。 如需有關 **text in row** 選項的詳細資訊，請參閱 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)。 如需有關讓文字指標變成無效的詳細資訊，請參閱 [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)。  
  
如果 @@TEXTSIZE 函式的值小於為 READTEXT 指定的大小，它就會取代為 READTEXT 指定的大小。 @@TEXTSIZE 函式會指定對 SET TEXTSIZE 陳述式所設定之傳回資料位元組數目的限制。 如需有關如何設定 TEXTSIZE 之工作階段設定的詳細資訊，請參閱 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
READTEXT 權限預設為授與有指定資料表之 SELECT 權限的使用者。 當傳送 SELECT 權限時，可以傳送權限。  
  
## <a name="examples"></a>範例  
下列範例會讀取 `pub_info` 資料表中 `pr_info` 資料行的第 2 到第 26 個字元。  
  
> [!NOTE]  
>  若要執行這個範例，您必須安裝 **pubs** 範例資料庫。  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr INNER JOIN publishers p  
      ON pr.pub_id = p.pub_id   
      AND p.pub_name = 'New Moon Books'  
READTEXT pub_info.pr_info @ptrval 1 25;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
