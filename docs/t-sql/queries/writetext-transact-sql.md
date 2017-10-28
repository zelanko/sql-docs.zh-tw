---
title: "WRITETEXT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5bf092ec05c2ae07864c12f092cf8b98f97234fa
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  允許進行最低限度記錄的互動式更新現有**文字**， **ntext**，或**映像**資料行。 WRITETEXT 會覆寫它所影響之資料行中的任何現有資料。 上不能使用 WRITETEXT**文字**， **ntext**，和**映像**檢視中的資料行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用大數值資料類型和**。**WRITE 子句[更新](../../t-sql/queries/update-transact-sql.md)陳述式改為。  
  
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
  
 *資料表* **.column**  
 這是資料表的名稱和**文字**， **ntext**，或**映像**来更新資料行。 資料表和資料行名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 資料庫名稱和擁有者名稱的指定是選擇性的。  
  
 *text_ptr*  
 已儲存的指標值**文字**， **ntext**，或**映像**資料。 *text_ptr*必須**binary （16)**。若要建立文字指標，執行[插入](../../t-sql/statements/insert-transact-sql.md)或[更新](../../t-sql/queries/update-transact-sql.md)陳述式不是 null 的資料搭配**文字**， **ntext**，或**映像**資料行。  
  
 WITH LOG  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會忽略這個項目。 記錄取決於資料庫的實際復原模式。  
  
 *資料*  
 是實際**文字**， **ntext**或**映像**来儲存資料。 *資料*可以是常值或參數。 可利用 WRITETEXT 以互動方式插入文字的最大長度大約是 120 KB 的**文字**， **ntext**，和**映像**資料。  
  
## <a name="remarks"></a>備註  
 利用 WRITETEXT 來取代**文字**， **ntext**，和**映像**資料，利用 UPDATETEXT 來修改**文字**， **ntext**，和**映像**資料。 UPDATETEXT 則更具彈性，因為它會變更的一部分**文字**， **ntext**，或**映像**而非整個資料行的資料行。  
  
 我們建議，為了達到最佳效能**文字**， **ntext**，和**映像**資料插入或更新以 8040 位元組倍數的大小。  
  
 如果資料庫復原模式是簡單或大量記錄**文字**， **ntext**，和**映像**新資料時，使用 WRITETEXT 作業是最低限度記錄的作業插入或附加。  
  
> [!NOTE]  
>  當更新現有的值時，不會使用最低限度記錄。  
  
 若要使 WRITETEXT 正確運作，資料行必須已包含有效的文字指標。  
  
 如果資料表沒有資料列文字[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]節省空間，不會初始化**文字**資料行中加入明確或隱含的 null 值時**文字**沒有文字指標與 INSERT 資料行可以是取得這些 null。 初始化**文字**資料行設為 NULL，使用 UPDATE 陳述式。 如果資料表有資料列文字，您就不需要初始化 Null 的文字資料行，一律能夠取得文字指標。  
  
 ODBC SQLPutData 函式會比較快，而且會使用動態記憶體比 WRITETEXT 少。 此函式可以插入 2 gb 的**文字**， **ntext**，或**映像**資料。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請在資料列文字指標**文字**， **ntext**，或**映像**資料可能存在而無效。 Text in row 選項的相關資訊，請參閱[sp_tableoption &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 如需讓文字指標無效的資訊，請參閱[sp_invalidate_textptr &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
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
 [UPDATETEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  

