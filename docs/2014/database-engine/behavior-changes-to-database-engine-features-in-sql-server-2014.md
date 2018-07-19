---
title: 行為變更至資料庫引擎的 SQL Server 2014 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- behavior changes [SQL Server]
- Database Engine [SQL Server], what's new
- Transact-SQL behavior changes
ms.assetid: 65eaafa1-9e06-4264-b547-cbee8013c995
caps.latest.revision: 134
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d83d502ec6b384a7c3e6a5f4ee2f4e7787ead4da
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193958"
---
# <a name="behavior-changes-to-database-engine-features-in-sql-server-2014"></a>SQL Server 2014 中對於 Database Engine 功能的行為變更
  本主題描述 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中的行為變更。 行為變更會影響 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 功能的運作或互動方式 (相較於舊版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])。  
  
## <a name="behavior-changes-in-includesssql14includessssql14-mdmd"></a>中的行為變更 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，針對包含超過特定長度 (超過 4020 個字元) 之字串的 XML 文件進行查詢，可能會傳回不正確的結果。 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，這類查詢會傳回正確的結果。  
  
## <a name="behavior-changes-in-includesssql11includessssql11-mdmd"></a>中的行為變更 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="metadata-discovery"></a>中繼資料探索  
 改進[!INCLUDE[ssDE](../includes/ssde-md.md)]開頭[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]允許以取得更精確的預期的結果描述比在舊版中傳回 SQLDescribeCol SQLDescribeCol [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 中繼資料探索](../relational-databases/native-client/features/metadata-discovery.md)。  
  
 [SET FMTONLY](/sql/t-sql/statements/set-fmtonly-transact-sql)選項，來判斷回應格式，不會取代實際執行查詢[sp_describe_first_result_set &#40;-&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql)， [sp_describe_undeclared_parameters &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql)， [sys.dm_exec_describe_first_result_set &#40;-&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql)，和[sys.dm_exec_describe_first_result_set_for_object &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql)。  
  
### <a name="changes-to-behavior-in-scripting-a-sql-server-agent-task"></a>編寫 SQL Server Agent 工作之指令碼時的行為變更  
 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，如果您透過從現有的作業複製指令碼來建立新的作業，新的作業可能會對現有的作業產生不良的影響。 若要建立新的工作，使用來自現有工作的指令碼，以手動方式刪除參數*@schedule_uid*而這通常是可在 現有的工作中建立作業排程之區段的最後一個參數。 這將會為新的作業建立新的獨立排程，而不會影響現有的作業。  
  
### <a name="constant-folding-for-clr-user-defined-functions-and-methods"></a>CLR 使用者定義函數和方法的常數摺疊  
 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，下列使用者定義的 CLR 物件現在是可摺疊的：  
  
-   具決定性、純量值的 CLR 使用者定義函數。  
  
-   CLR 使用者定義類型的具決定性方法。  
  
 此改進旨在於這些函數或方法都使用相同的引數多次呼叫時提高效能。 但在不具決定性函數或方法因誤標記為具決定性時，此變更可能會導致非預期的結果。 CLR 函數或方法的決定性是由 `IsDeterministic` 或 `SqlFunctionAttribute` 的 `SqlMethodAttribute` 屬性值所指出。  
  
### <a name="behavior-of-stenvelope-method-has-changed-with-empty-spatial-types"></a>空白空間類型之 STEnvelope() 方法的行為已變更  
 具有空白物件之 `STEnvelope` 方法的行為現在與其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 空間方法的行為一致。  
  
 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，以空白物件呼叫 `STEnvelope` 方法時，此方法傳回下列結果：  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns POINT EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns LINESTRING EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns POLYGON EMPTY  
```  
  
 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，以空白物件呼叫 `STEnvelope` 方法時，此方法現在傳回下列結果：  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
```  
  
 若要判斷空間物件是否為空白，請呼叫[STIsEmpty &#40;geometry 資料類型&#41;](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type)方法。  
  
### <a name="log-function-has-new-optional-parameter"></a>LOG 函數有新的選擇性參數  
 `LOG`函式現在有一個選擇性*基底*參數。 如需詳細資訊，請參閱 <<c0> [ 記錄&#40;TRANSACT-SQL&#41;](/sql/t-sql/functions/log-transact-sql)。</c0>  
  
### <a name="statistics-computation-during-partitioned-index-operations-has-changed"></a>分割區索引作業期間的統計資料計算已變更  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 並不會在建立或重建分割區索引之後掃描資料表中所有的資料列建立統計資料。 反之，查詢最佳化工具會使用預設的採樣演算法來產生統計資料。 升級具有分割區索引的資料庫之後，可能會注意到這些索引之長條圖資料的差異。 此行為變更可能不會影響查詢效能。 如果要在掃描資料表中所有資料列時取得分割區索引的統計資料，請使用 CREATE STATISTICS 或 UPDATE STATISTICS 搭配 FULLSCAN 子句。  
  
### <a name="data-type-conversion-by-the-xml-value-method-has-changed"></a>XML value 方法的資料類型轉換已變更  
 `value`資料類型之 `xml`方法的內部行為已變更。 此方法會針對 XML 執行 XQuery 並傳回指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型的純量值。 xs 類型必須轉換為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型。 以前 `value` 方法會在內部將來源值轉換為 xs:string，然後將 xs:string 轉換為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型。 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，下列情況下會略過 xs:string 的轉換：  
  
|來源 XS 資料類型|目的地 SQL Server 資料類型|  
|-------------------------|--------------------------------------|  
|byte<br /><br /> short<br /><br /> ssNoversion<br /><br /> integer<br /><br /> long<br /><br /> unsignedByte<br /><br /> unsignedShort<br /><br /> unsignedInt<br /><br /> unsignedLong<br /><br /> positiveInteger<br /><br /> nonPositiveInteger<br /><br /> negativeInteger<br /><br /> nonNegativeInteger|TINYINT<br /><br /> SMALLINT<br /><br /> ssNoversion<br /><br /> BIGINT<br /><br /> Decimal<br /><br /> NUMERIC|  
|Decimal|Decimal<br /><br /> NUMERIC|  
|FLOAT|REAL|  
|double|FLOAT|  
  
 可以略過中繼轉換時，新行為會提高效能。 但在資料類型轉換失敗時，您會看到不同於從中繼 xs:string 值轉換時所引發的錯誤訊息。 例如，如果 value 方法無法將 `int` 值 100000 轉換為 `smallint`，以前的錯誤訊息是：  
  
 `The conversion of the nvarchar value '100000' overflowed an INT2 column. Use a larger integer column.`  
  
 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]，如果沒有 xs:string 的中繼轉換，錯誤訊息是：  
  
 `Arithmetic overflow error converting expression to data type smallint.`  
  
### <a name="sqlcmdexe-behavior-change-in-xml-mode"></a>XML 模式中的 sqlcmd.exe 行為變更  
 如果您在執行 SELECT * from T FOR XML ... 時，搭配 XML 模式 (:XML ON 命令) 使用 sqlcmd.exe，會發生行為變更。  
  
### <a name="dbcc-checkident-revised-message"></a>DBCC CHECKIDENT 修訂的訊息  
 在  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]，DBCC CHECKIDENT 命令所傳回的訊息已變更只與重新植入使用時*new_reseed_value*若要變更目前的識別值。 新的訊息是 「 正在檢查識別資訊： 目前識別值 '\<目前識別值 >'。 DBCC 的執行已經完成。 如果 DBCC 印出錯誤訊息，請連絡您的系統管理員」。  
  
 在舊版中，訊息是 「 正在檢查識別資訊： 目前識別值 '\<目前的識別值 >'，目前的資料行值'\<目前的資料行值 >'。 DBCC 的執行已經完成。 如果 DBCC 印出錯誤訊息，請連絡您的系統管理員」。 搭配 NORESEED 指定了 DBCC CHECKIDENT，但沒有第二個參數或沒有 reseed 值時，訊息保持不變。 如需詳細資訊，請參閱 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)。  
  
### <a name="behavior-of-exist-function-on-xml-datatype-has-changed"></a>XML 資料類型上之 exist() 函數的行為已變更  
 行為**exist （)** 比較具有 null 值為 0 （零） 的 XML 資料類型時，函式已變更。 請設想下列範例：  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 0;  
```  
  
 在舊版中，此比較傳回 1 (true)；現在，此比較傳回 0 (零，false)。  
  
 下列比較尚未變更：  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 1; -- 0 expected, 0 returned  
SELECT COUNT(1) WHERE @test.exist('/dogs') IS NULL; -- 1 expected, 1 returned  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中的 Database Engine 功能的重大變更](breaking-changes-to-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中已被取代的 Database Engine 功能](deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中已停止的 Database Engine 功能](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
