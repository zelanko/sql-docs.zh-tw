---
title: WRITETEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WRITETEXT_TSQL
- WRITETEXT
dev_langs:
- TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fda340750c555d7e6e858ddac1a87401e215891e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  允許以記錄最少資訊的互動方式，更新現有的 **text**、**ntext** 或 **image** 資料行。 WRITETEXT 會覆寫它所影響之資料行中的任何現有資料。 WRITETEXT 不能用在檢視表中的 **text**、**ntext** 及 **image** 資料行上。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用大數值資料類型和 [UPDATE](../../t-sql/queries/update-transact-sql.md) 陳述式的 **.**WRITE 子句。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
WRITETEXT [BULK]  
  { table.column text_ptr }  
  [ WITH LOG ] { data }  
```  
  
## <a name="arguments"></a>引數  
 BULK  
 讓上傳工具能夠上傳二進位資料流。 此資料流必須由位於 TDS 通訊協定層級的工具提供。 當資料流不存在時，查詢處理器就會忽略 BULK 選項。  
  
> [!IMPORTANT]  
>  我們建議您不要將 BULK 選項用於以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為基礎的應用程式中。 未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本可能會變更或移除這個選項。  
  
 *table* **.column**  
 這是要更新之資料表及 **text**、**ntext** 或 **image** 資料行的名稱。 資料表和資料行名稱必須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。 資料庫名稱和擁有者名稱的指定是選擇性的。  
  
 *text_ptr*  
 這是儲存 **text**、**ntext** 或 **image** 資料之指標的值。 *text_ptr* 必須是 **binary(16)**。若要建立文字指標，請搭配 **text**、**ntext** 或 **image** 資料行並非 Null 的資料來執行 [INSERT](../../t-sql/statements/insert-transact-sql.md) 或 [UPDATE](../../t-sql/queries/update-transact-sql.md) 陳述式。  
  
 WITH LOG  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會忽略這個項目。 記錄取決於資料庫的實際復原模式。  
  
 *data*  
 這是要儲存的實際 **text**、**ntext** 或 **image** 資料。 *data* 可以是常值或參數。 就 **text**、**ntext** 及 **image** 資料而言，可使用 WRITETEXT 以互動方式插入的文字長度上限大約是 120 KB。  
  
## <a name="remarks"></a>Remarks  
 請使用 WRITETEXT 來取代 **text**、**ntext** 及 **image** 資料，使用 UPDATETEXT 來修改 **text**、**ntext** 及 **image** 資料。 UPDATETEXT 較有彈性，因為它只會變更 **text**、**ntext** 或 **image** 資料行的一部份，而不是變更整個資料行。  
  
 為了獲得最佳效能，建議您以 8040 個位元組之倍數的片段大小來插入或更新 **text**、**ntext** 及 **image** 資料。  
  
 如果資料庫復原模式為簡單或大量記錄模式，當插入或附加新資料時，使用 WRITETEXT 的 **text**、**ntext** 及 **image** 作業會是記錄最少資訊的作業。  
  
> [!NOTE]  
>  當更新現有的值時，不會使用最低限度記錄。  
  
 若要使 WRITETEXT 正確運作，資料行必須已包含有效的文字指標。  
  
 如果資料表沒有同資料列文字，當使用 INSERT 在 **text** 資料行中新增明確或隱含的 Null 值，而無法取得這些 Null 的文字指標時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會藉由不將 **text** 資料行初始化來節省空間。 若要將 **text** 資料行初始化成 NULL，請使用 UPDATE 陳述式。 如果資料表有資料列文字，您就不需要初始化 Null 的文字資料行，一律能夠取得文字指標。  
  
 與 WRITETEXT 相比，ODBC SQLPutData 函數的處理速度較快，且使用的動態記憶體較少。 此函數最多可插入 2 GB 的 **text**、**ntext** 或 **image** 資料。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，可能有指向 **text**、**ntext** 或 **image** 資料的同資料列文字指標存在，但可能無效。 如需有關 text in row 選項的資訊，請參閱[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)。 如需有關讓文字指標變成無效的資訊，請參閱 [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要指定之資料表的 UPDATE 權限。 當傳送 UPDATE 權限時，可以傳送權限。  
  
## <a name="examples"></a>範例  
 下列範例將文字指標放在區域變數 `@ptrval` 中，再利用 `WRITETEXT`，將新的文字字串放入 `@ptrval` 所指向的資料列中。  
  
> [!NOTE]  
>  若要執行這個範例，您必須安裝 pubs 範例資料庫。  
  
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
WRITETEXT pub_info.pr_info @ptrval 'New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!';  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
