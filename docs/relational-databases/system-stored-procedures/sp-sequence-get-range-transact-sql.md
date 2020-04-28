---
title: sp_sequence_get_range （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd17110b5a5f2abf8f64662221f334ebf769b258
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "77114564"
---
# <a name="sp_sequence_get_range-transact-sql"></a>sp_sequence_get_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  從順序物件傳回順序值的範圍。 順序物件會產生及發出要求的值數目，並將範圍相關的中繼資料提供給應用程式。  
  
 如需序號的詳細資訊，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
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
`[ @sequence_name = ] N'sequence'`順序物件的名稱。 此結構描述是選擇性的。 *sequence_name*是**Nvarchar （776）**。  
  
`[ @range_size = ] range_size`要從序列中提取的值數目。 range_size 是**Bigint**。 ** \@ **  
  
`[ @range_first_value = ] range_first_value`Output 參數會傳回用來計算要求範圍之順序物件的第一個（最小或最大）值。 range_first_value 的**SQL_variant** ，其基底類型與要求中所用順序物件的相同。 ** \@ **  
  
`[ @range_last_value = ] range_last_value`選擇性輸出參數會傳回所要求範圍的最後一個值。 range_last_value 的**SQL_variant** ，其基底類型與要求中所用順序物件的相同。 ** \@ **  
  
`[ @range_cycle_count = ] range_cycle_count`選擇性輸出參數會傳回順序物件為了傳回要求的範圍而迴圈的次數。 range_cycle_count 為**int**。 ** \@ **  
  
`[ @sequence_increment = ] sequence_increment`選擇性輸出參數會傳回用來計算所要求範圍之順序物件的增量。 sequence_increment 的**SQL_variant** ，其基底類型與要求中所用順序物件的相同。 ** \@ **  
  
`[ @sequence_min_value = ] sequence_min_value`選擇性輸出參數會傳回順序物件的最小值。 sequence_min_value 的**SQL_variant** ，其基底類型與要求中所用順序物件的相同。 ** \@ **  
  
`[ @sequence_max_value = ] sequence_max_value`選擇性輸出參數會傳回順序物件的最大值。 sequence_max_value 的**SQL_variant** ，其基底類型與要求中所用順序物件的相同。 ** \@ **  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 在 sys 中 sp_sequence_get_rangeis。 架構和可以參考為 sys.databases sp_sequence_get_range。  
  
### <a name="cycling-sequences"></a>循環的順序  
 必要時，順序物件會以適當次數循環，以提供要求的範圍。 循環次數是透過 `@range_cycle_count` 參數傳回給呼叫端。  
  
> [!NOTE]  
>  循環時，順序物件會從遞增順序的最小值以及遞減順序的最大值重新啟動，而不是從順序物件的開始值重新啟動。  
  
### <a name="non-cycling-sequences"></a>非循環的順序  
 如果在要求範圍內的值數目大於順序物件中的剩餘可用值，則不會從順序物件扣除要求範圍，而是會傳回下列錯誤 11732：  
  
 `The requested range for sequence object '%.*ls' exceeds the maximum or minimum limit. Retry with a smaller range.`  
  
## <a name="permissions"></a>權限  
 需要順序物件或順序物件之結構描述的 UPDATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會使用名為 RangeSeq 的順序物件。 使用下列語句來建立 RangeSeq 序列。  
  
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
 下列語句會從 RangeSeq 序列物件取得四個序號，並將第一個數位傳回給使用者。  
  
```  
DECLARE @range_first_value_output sql_variant ;  
  
EXEC sys.sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 4  
, @range_first_value = @range_first_value_output OUTPUT ;  
  
SELECT @range_first_value_output AS FirstNumber ;  
  
```  
  
### <a name="b-returning-all-output-parameters"></a>B. 傳回所有輸出參數  
 下列範例會從 sp_sequence_get_range 程式傳回所有輸出值。  
  
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
 下列範例會使用 ADO.NET 從 RangeSeq 取得範圍。  
  
```  
SqlCommand cmd = new SqlCommand();  
cmd.Connection = conn;  
cmd.CommandType = CommandType.StoredProcedure;  
cmd.CommandText = "sys.sp_sequence_get_range";  
cmd.Parameters.AddWithValue("@sequence_name", "Test.RangeSeq");  
cmd.Parameters.AddWithValue("@range_size", 10);  
  
// Specify an output parameter to retrieve the first value of the generated range.  
SqlParameter firstValueInRange = new SqlParameter("@range_first_value", SqlDbType.Variant);  
firstValueInRange.Direction = ParameterDirection.Output;  
cmd.Parameters.Add(firstValueInRange);  
  
conn.Open();  
cmd.ExecuteNonQuery();  
  
// Output the first value of the generated range.  
Console.WriteLine(firstValueInRange.Value);  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SEQUENCE &#40;Transact-sql&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-sql&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-sql&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [&#40;Transact-sql&#41;的下一個值](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
