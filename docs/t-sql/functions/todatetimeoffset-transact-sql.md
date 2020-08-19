---
description: TODATETIMEOFFSET (Transact-SQL)
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5274a17e4de005c3947aba96956b62b5d200409
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459530"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回從 **datetime2** 運算式翻譯的 **datetimeoffset** 值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *expression*  
 為解析為 [datetime2](../../t-sql/data-types/datetime2-transact-sql.md) 值的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
> [!NOTE]  
>  運算式的類型不可為 **text**、**ntext** 或 **image**，因為這些類型不可隱含轉換成 **varchar** 或 **nvarchar**。  
  
 *time_zone*  
 這是代表時區時差的運算式，以分鐘為單位 (若為整數)，例如 -120，或以小時和分鐘為單位 (若為字串)，例如 '+13:00'。 範圍是 +14 到 -14 (以小時為單位)。 此運算式會針對指定的 time_zone 以當地時間解譯。  
  
> [!NOTE]  
>  如果運算式為字元字串，它的格式必須為 {+|-}TZH:THM。  
  
## <a name="return-type"></a>傳回類型  
 **datetimeoffset**. 毫秒精確度與 *datetime* 引數相同。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. 變更目前日期和時間的時區時差  
 下列範例會將目前日期和時間的時區時差變更為 `-07:00` 時區。  
  
```sql  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2019-04-22 16:23:51.7666667 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. 變更時區時差 (以分鐘為單位)  
 下列範例會將目前的時區變更為 `-120` 分鐘。  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), -120)
-- RETURNS: 2019-04-22 11:39:21.6986813 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. 在時區時差中增加 13 小時的時間  
 下列範例會在日期和時間中加入 13 小時的時區時差。  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), '+13:00')
-- RETURNS: 2019-04-22 11:39:29.0339301 +13:00
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日期和時間資料類型與函式 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

