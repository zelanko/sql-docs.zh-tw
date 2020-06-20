---
title: 支援的資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
author: rothja
ms.author: jroth
ms.openlocfilehash: a7dda500486c39a66f871d5934f957028fc51e9d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025735"
---
# <a name="supported-data-types"></a>支援的資料類型
  記憶體最佳化的資料表及原生編譯預存程序 **支援** 下列資料類型：  
  
 **數值資料類型**  
  
|資料類型|取得詳細資訊|  
|---------------|--------------------------|  
|int|[int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|BIGINT|[int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|SMALLINT|[int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|TINYINT|[int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|decimal|[decimal 和 numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|NUMERIC|[decimal 和 numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|FLOAT|[float 和 real &#40;Transact-SQL&#41;](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|real|[float 和 real &#40;Transact-SQL&#41;](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|money|[money 和 smallmoney &#40;Transact-SQL&#41;](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
|SMALLMONEY|[money 和 smallmoney &#40;Transact-SQL&#41;](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
  
 **字串資料類型**  
  
|資料類型|取得詳細資訊|  
|---------------|--------------------------|  
|char(n)|[char 和 varchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|Varchar （n） <sup>1</sup>|[char 和 varchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|nchar(n)|[nchar 和 nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|Nvarchar （n） <sup>1</sup>|[nchar 和 nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|sysname|[nchar 和 nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
  
 <sup>1</sup>限制為每個資料列總計8060個位元組，在可變長度的類型中計算（n）。  
  
 如需支援之定序的資訊，請參閱＜ [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)＞。  
  
 **日期和時間資料類型**  
  
|資料類型|取得詳細資訊|  
|---------------|--------------------------|  
|date|[日期 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/date-transact-sql)|  
|time|[time &#40;Transact-SQL&#41;](/sql/t-sql/data-types/time-transact-sql)|  
|Datetime|[datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql)|  
|datetime2|[datetime2 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime2-transact-sql)|  
|smalldatetime|[smalldatetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/smalldatetime-transact-sql)|  
  
 **二進位資料類型**  
  
|資料類型|取得詳細資訊|  
|---------------|--------------------------|  
|bit|[bit &#40;Transact-SQL&#41;](/sql/t-sql/data-types/bit-transact-sql)|  
|binary(n)|[binary 和 varbinary &#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
|Varbinary （n） <sup>1</sup>|[binary 和 varbinary &#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
  
 <sup>1</sup>限制為每個資料列總計8060個位元組，在可變長度的類型中計算（n）。  
  
 **其他資料類型**  
  
|資料類型|取得詳細資訊|  
|---------------|--------------------------|  
|UNIQUEIDENTIFIER|[uniqueidentifier &#40;Transact-SQL&#41;](/sql/t-sql/data-types/uniqueidentifier-transact-sql)|  
  
 **不支援的資料類型**  
  
 以下是不支援的資料類型：  
  
||||  
|-|-|-|  
|DATETIMEOFFSET|GEOGRAPHY|GEOMETRY|  
|HIERARCHYID|大型物件 (LOB)。 例如，varchar(max)、nvarchar(max)、varbinary(max)、影像、xml、文字和 ntext。|ROWVERSION|  
|sql_variant|CLR 函數|使用者定義型別 (UDT)|  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP 的 transact-sql 支援](transact-sql-support-for-in-memory-oltp.md)   
 [在記憶體優化資料表中執行 LOB 資料行](../../database-engine/implementing-lob-columns-in-a-memory-optimized-table.md)   
 [在記憶體最佳化資料表中實作 SQL_VARIANT](implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  
