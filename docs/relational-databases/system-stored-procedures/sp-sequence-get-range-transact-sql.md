---
title: sp_sequence_get_range (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_sequence_get_range
- sp_sequence_get_range_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sp_sequence_get_range procedure
- sp_sequence_get_range
ms.assetid: 8ca6b0c6-8d9c-4eee-b02f-51ddffab4492
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5171d32c6aec0f1bbd23a17824a61964182666e0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066501"
---
# <a name="spsequencegetrange-transact-sql"></a>sp_sequence_get_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  從順序物件傳回順序值的範圍。 順序物件會產生及發出要求的值數目，並將範圍相關的中繼資料提供給應用程式。  
  
 如有關序號的詳細資訊，請參閱 <<c0> [ 序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_sequence_get_range [ @sequence_name = ] N'<sequence>'   
     , [ @range_size = ] range_size  
     , [ @range_first_value = ] range_first_value OUTPUT   
    [, [ @range_last_value = ] range_last_value OUTPUT ]  
    [, [ @range_cycle_count = ] range_cycle_count OUTPUT ]  
    [, [ @sequence_increment = ] sequence_increment OUTPUT ]  
    [, [ @sequence_min_value = ] sequence_min_value OUTPUT ]  
    [, [ @sequence_max_value = ] sequence_max_value OUTPUT ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@sequence_name** =] **N**'*序列*'  
 順序物件的名稱。 此結構描述是選擇性的。 *sequence_name*已**nvarchar(776)**。  
  
 [ **@range_size** =] *range_size*  
 要從順序擷取的值數目。 **@range_size** 已**bigint**。  
  
 [ **@range_first_value** = ] *range_first_value*  
 輸出參數會傳回用以計算要求範圍的順序物件之第一個值 (最小值或最大值)。 **@range_first_value** 已**sql_variant**與要求中使用順序物件的基底類型相同。  
  
 [ **@range_last_value** = ] *range_last_value*  
 選擇性輸出參數會傳回所要求的範圍的最後一個值。 **@range_last_value** 已**sql_variant**與要求中使用順序物件的基底類型相同。  
  
 [ **@range_cycle_count** =] range_cycle_count  
 選擇性輸出參數會傳回順序物件循環次數，以傳回要求的範圍。 **@range_cycle_count** 已**int**。  
  
 [ **@sequence_increment** = ] *sequence_increment*  
 選擇性輸出參數會傳回順序物件的增量，用來計算要求的範圍。 **@sequence_increment** 已**sql_variant**與要求中使用順序物件的基底類型相同。  
  
 [ **@sequence_min_value** = ] *sequence_min_value*  
 選擇性輸出參數會傳回順序物件的最小值。 **@sequence_min_value** 已**sql_variant**與要求中使用順序物件的基底類型相同。  
  
 [ **@sequence_max_value** = ] *sequence_max_value*  
 選擇性輸出參數會傳回順序物件的最大值。 **@sequence_max_value** 已**sql_variant**與要求中使用順序物件的基底類型相同。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 在 sys sp_sequence_get_rangeis。 結構描述，而且可以當做 sys.sp_sequence_get_range 參考。  
  
### <a name="cycling-sequences"></a>循環的順序  
 必要時，順序物件會以適當次數循環，以提供要求的範圍。 循環次數是透過 `@range_cycle_count` 參數傳回給呼叫端。  
  
> [!NOTE]  
>  循環時，順序物件會從遞增順序的最小值以及遞減順序的最大值重新啟動，而不是從順序物件的開始值重新啟動。  
  
### <a name="non-cycling-sequences"></a>非循環的順序  
 如果在要求範圍內的值數目大於順序物件中的剩餘可用值，則不會從順序物件扣除要求範圍，而是會傳回下列錯誤 11732：  
  
 `The requested range for sequence object '%.*ls' exceeds the maximum or minimum limit. Retry with a smaller range.`  
  
## <a name="permissions"></a>Permissions  
 需要順序物件或順序物件之結構描述的 UPDATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會使用名為 Test.RangeSeq 的順序物件。 您可以使用下列陳述式來建立 Test.RangeSeq 順序。  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.RangeSeq  
    AS int   
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 25  
    CYCLE  
    CACHE 10  
;  
```  
  
### <a name="a-retrieving-a-range-of-sequence-values"></a>A. 擷取序列值的範圍  
 下列陳述式從 Test.RangeSeq 順序物件取得四個序號，並傳回數字的第一個給使用者。  
  
```  
DECLARE @range_first_value sql_variant ,   
        @range_first_value_output sql_variant ;  
  
EXEC sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 4  
, @range_first_value = @range_first_value_output OUTPUT ;  
  
SELECT @range_first_value_output AS FirstNumber ;  
  
```  
  
### <a name="b-returning-all-output-parameters"></a>B. 傳回所有輸出參數  
 下列範例會傳回所有輸出值，從 sp_sequence_get_range 程序。  
  
```  
DECLARE    
  @FirstSeqNum sql_variant  
, @LastSeqNum sql_variant  
, @CycleCount int  
, @SeqIncr sql_variant  
, @SeqMinVal sql_variant  
, @SeqMaxVal sql_variant ;  
  
EXEC sys.sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 5  
, @range_first_value = @FirstSeqNum OUTPUT   
, @range_last_value = @LastSeqNum OUTPUT   
, @range_cycle_count = @CycleCount OUTPUT  
, @sequence_increment = @SeqIncr OUTPUT  
, @sequence_min_value = @SeqMinVal OUTPUT  
, @sequence_max_value = @SeqMaxVal OUTPUT ;  
  
-- The following statement returns the output values  
SELECT  
  @FirstSeqNum AS FirstVal  
, @LastSeqNum AS LastVal  
, @CycleCount AS CycleCount  
, @SeqIncr AS SeqIncrement  
, @SeqMinVal AS MinSeq  
, @SeqMaxVal AS MaxSeq ;  
  
```  
  
 將 `@range_size` 引數變更為大數值 (例如 75) 會造成順序物件循環。 請檢查 `@range_cycle_count` 引數，以判斷順序物件是否已循環以及循環次數。  
  
### <a name="c-example-using-adonet"></a>C. 使用 ADO.NET 的範例  
 下列範例使用 ADO.NET，從 Test.RangeSeq 取得範圍。  
  
```  
SqlCommand cmd = new SqlCommand();  
cmd.Connection = conn;  
cmd.CommandType = CommandType.StoredProcedure;  
cmd.CommandText = "sys.sp_sequence_get_range";  
cmd.Parameters.AddWithValue("@sequence_name", "Test.RangeSeq");  
cmd.Parameters.AddWithValue("@range_size", 10);  
  
// Specify an output parameter to retreive the first value of the generated range.  
SqlParameter firstValueInRange = new SqlParameter("@range_first_value", SqlDbType.Variant);  
firstValueInRange.Direction = ParameterDirection.Output;  
cmd.Parameters.Add(firstValueInRange);  
  
conn.Open();  
cmd.ExecuteNonQuery();  
  
// Output the first value of the generated range.  
Console.WriteLine(firstValueInRange.Value);  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
