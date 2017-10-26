---
title: "READTEXT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c501fe8ea8146b4b2ec6e138f72fc2604b4b374
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  讀取**文字**， **ntext**，或**映像**值從**文字**， **ntext**，或**映像**資料行，從指定位移開始，讀取指定的位元組數目。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[SUBSTRING](../../t-sql/functions/substring-transact-sql.md)函式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>引數  
 *資料表* **。** *資料行*  
 這是要讀取的資料表和資料行名稱。 資料表和資料行名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 您必須指定資料表和資料行名稱；不過，資料庫名稱和擁有者名稱的指定是選擇性的。  
  
 *text_ptr*  
 這是一個有效的文字指標。 *text_ptr*必須**binary （16)**。  
  
 *位移*  
 是位元組數 (時**文字**或**映像**資料類型可用) 或字元 (當**ntext**使用的資料類型) 略過之後，才能開始讀取**文字**，**映像**，或**ntext**資料。  
  
 *大小*  
 是位元組數 (時**文字**或**映像**資料類型可用) 或字元 (當**ntext**使用的資料類型) 的可讀取的資料。 如果*大小*為 0，讀取 4 KB 位元組的資料。  
  
 HOLDLOCK  
 造成讀取文字值的鎖定，直到交易結束為止。 其他使用者可以讀取值，但他們無法修改它。  
  
## <a name="remarks"></a>備註  
 使用[TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)函式可取得有效*text_ptr*值。 TEXTPTR 會傳回指標**文字**， **ntext**，或**映像**資料行中指定的資料列或**文字**， **ntext**，或**映像**如果傳回多個資料列，查詢所傳回的最後一個資料列中的資料行。 由於 TEXTPTR 會傳回 16 位元組二進位字串，我們建議您宣告一個本機變數來存放文字指標，再搭配 READTEXT 來使用這個變數。 如需有關宣告本機變數的詳細資訊，請參閱[DECLARE @local_variable &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，同資料列文字指標有可能存在而無效。 如需有關**資料列中的文字**選項，請參閱[sp_tableoption &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 如需有關讓文字指標無效的詳細資訊，請參閱[sp_invalidate_textptr &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 值 @@TEXTSIZE函數會取代指定給 READTEXT，如果它小於 READTEXT 的指定大小的大小。 @@TEXTSIZE函式的 SET TEXTSIZE 陳述式所傳回集合的資料位元組數指定的限制。 如需如何設定 textsize 之工作階段設定的詳細資訊，請參閱[SET TEXTSIZE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 READTEXT 權限預設為授與有指定資料表之 SELECT 權限的使用者。 當傳送 SELECT 權限時，可以傳送權限。  
  
## <a name="examples"></a>範例  
 下列範例會讀取 `pr_info` 資料表中 `pub_info` 資料行的第 2 到 26 個字元。  
  
> [!NOTE]  
>  若要執行此範例中，您必須安裝**pubs**範例資料庫。  
  
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
  
  

