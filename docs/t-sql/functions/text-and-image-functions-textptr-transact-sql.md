---
title: "TEXTPTR (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTPTR_TSQL
- TEXTPTR
dev_langs: TSQL
helpviewer_keywords:
- TEXTPTR function
- viewing text pointer values
- text-pointer values
- displaying text pointer values
ms.assetid: 2672b8cb-f747-46f3-9358-9b49b3583b8e
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 109f9bdd06bf27928450c89ad06dc6d93247b881
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="text-and-image-functions---textptr-transact-sql"></a>文字和影像函數-TEXTPTR (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回文字指標值，對應為**文字**， **ntext**，或**映像**中的資料行**varbinary**格式。 擷取的文字指標值可用在 READTEXT、WRITETEXT 和 UPDATETEXT 陳述式中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]無法使用替代功能。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
TEXTPTR ( column )  
```  
  
## <a name="arguments"></a>引數  
 *資料行*  
 是**文字**， **ntext**，或**映像**將使用的資料行。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary**  
  
## <a name="remarks"></a>備註  
 如果是含同資料列文字的資料表，TEXTPTR 會傳回要處理之文字的控制代碼。 即使文字值是 NULL，您也可以取得有效的文字指標。  
  
 在檢視的資料行上無法使用 TEXTPTR 函數。 您只能將它用於資料表資料行。 若要檢視的資料行上使用 TEXTPTR 函數，您必須設定相容性層級為 80 使用[ALTER DATABASE 相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。 如果資料表沒有同資料列文字，而且如果**文字**， **ntext**，或**映像**UPDATETEXT 陳述式尚未初始化資料行，TEXTPTR 會傳回 null 指標。  
  
 請利用 TEXTVALID 來測試文字指標是否存在。 如果有效的文字指標不存在，您便無法使用 UPDATETEXT、WRITETEXT 或 READTEXT。  
  
 這些函式和陳述式也很有用當您使用**文字**， **ntext**，和**映像**資料。  
  
|函數或陳述式|Description|  
|---------------------------|-----------------|  
|PATINDEX**('***%模式 %***'，** *運算式***)**|傳回指定的字元字串中的字元位置**文字**或**ntext**資料行。|  
|DATALENGTH**(***運算式***)**|傳回的資料長度**文字**， **ntext**，和**映像**資料行。|  
|SET TEXTSIZE|傳回的限制，以位元組為單位，**文字**， **ntext**，或**映像**SELECT 陳述式傳回的資料。|  
|子字串**(***text_column*，*啟動*，*長度***)**|傳回**varchar**指定所指定的字串*啟動*位移和*長度*。 長度應該小於 8 KB。|  
  
## <a name="examples"></a>範例  
  
> [!NOTE]  
>  若要執行下列的範例，您必須安裝**pubs**資料庫。  
  
### <a name="a-using-textptr"></a>A. 使用 TEXTPTR  
 下列範例會使用`TEXTPTR`函式來尋找**映像**資料行`logo`聯`New Moon Books`中`pub_info`資料表`pubs`資料庫。 這個文字指標放在本機變數 `@ptrval.` 中。  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(logo)  
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books';  
GO  
```  
  
### <a name="b-using-textptr-with-in-row-text"></a>B. 使用 TEXTPTR 搭配 in-row 文字  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，同資料列文字指標必須如下列範例所示，在交易內使用。  
  
```  
CREATE TABLE t1 (c1 int, c2 text);  
EXEC sp_tableoption 't1', 'text in row', 'on';  
INSERT t1 VALUES ('1', 'This is text.');  
GO  
BEGIN TRAN;  
   DECLARE @ptrval VARBINARY(16);  
   SELECT @ptrval = TEXTPTR(c2)  
   FROM t1  
   WHERE c1 = 1;  
   READTEXT t1.c2 @ptrval 0 1;  
COMMIT;  
```  
  
### <a name="c-returning-text-data"></a>C. 傳回文字資料  
 下列範例會從 `pub_id` 資料表中，選取 `pr_info` 資料行和 `pub_info` 資料行的 16 位元組文字指標。  
  
```  
USE pubs;  
GO  
SELECT pub_id, TEXTPTR(pr_info)  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id                                      
------ ----------------------------------   
0736   0x6c0000000000feffb801000001000100   
0877   0x6d0000000000feffb801000001000300   
1389   0x6e0000000000feffb801000001000500   
1622   0x700000000000feffb801000001000900   
1756   0x710000000000feffb801000001000b00   
9901   0x720000000000feffb801000001000d00   
9952   0x6f0000000000feffb801000001000700   
9999   0x730000000000feffb801000001000f00   
  
(8 row(s) affected)  
```  
  
 下列範例會顯示如何在不使用 TEXTPTR 的情況下，傳回文字的前 `8000` 位元組。  
  
```  
USE pubs;  
GO  
SET TEXTSIZE 8000;  
SELECT pub_id, pr_info  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id pr_info                                                                                                                                                                                                                                                           
------ -----------------------------------------------------------------  
0736   New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!                                                                                                             
0877   This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washington, D.C.  
  
This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washi   
1389   This is sample text data for Algodata Infosystems, publisher 1389 in the pubs database. Algodata Infosystems is located in Berkeley, California.  
  
9999   This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in Paris, France.  
  
This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in   
  
(8 row(s) affected)  
```  
  
### <a name="d-returning-specific-text-data"></a>D. 傳回特定文字資料  
 下列範例會找出`text`資料行 (`pr_info`) 相關聯`pub_id``0736`中`pub_info`資料表`pubs`資料庫。 它先宣告本機變數 `@val`。 之後，將文字指標 (大型二進位字串) 放在 `@val` 中，將它當作一個參數來提供給 `READTEXT` 陳述式。 這會傳回從第 5 位元組 (位移 4) 開始的 10 個位元組。  
  
```  
USE pubs;  
GO  
DECLARE @val varbinary(16);  
SELECT @val = TEXTPTR(pr_info)   
FROM pub_info  
WHERE pub_id = '0736';  
READTEXT pub_info.pr_info @val 4 10;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pr_info                                                                                                                                                                                                                                                           
-----------------------------------------------------------------------  
 is sample  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>請參閱＜  
 [DATALENGTH &#40;TRANSACT-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [READTEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [SET TEXTSIZE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [文字和影像函數 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
