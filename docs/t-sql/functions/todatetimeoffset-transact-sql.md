---
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 65a6cf2cb4fe4e65764b1ac2a86c4177f3f88637
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33057747"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回從 **datetime2** 運算式翻譯的 **datetimeoffset** 值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 為解析為 [datetime2](../../t-sql/data-types/datetime2-transact-sql.md) 值的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
> [!NOTE]  
>  運算式的類型不可為 **text**、**ntext** 或 **image**，因為這些類型不可隱含轉換成 **varchar** 或 **nvarchar**。  
  
 *time_zone*  
 這是代表時區時差的運算式，以分鐘為單位 (若為整數)，例如 -120，或以小時和分鐘為單位 (若為字串)，例如 ‘+13.00’。 範圍是 +14 到 -14 (以小時為單位)。 此運算式會針對指定的 time_zone 以當地時間解譯。  
  
> [!NOTE]  
>  如果運算式為字元字串，它的格式必須為 {+|-}TZH:THM。  
  
## <a name="return-type"></a>傳回類型  
 **datetimeoffset**. 毫秒精確度與 *datetime* 引數相同。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. 變更目前日期和時間的時區時差  
 下列範例會將目前日期和時間的時區時差變更為 `-07:00` 時區。  
  
```  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2007-08-30 15:51:34.7030000 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. 變更時區時差 (以分鐘為單位)  
 下列範例會將目前的時區變更為 `-120` 分鐘。  
  
```  
DECLARE @todaysDate datetime2;  
SET @todaysDate = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDate, -120);  
-- RETURNS 2007-08-30 15:52:37.8770000 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. 在時區時差中增加 13 小時的時間  
 下列範例會在日期和時間中加入 13 小時的時區時差。  
  
```  
DECLARE @dateTime datetimeoffset(7)= '2007-08-28 18:00:30';  
SELECT TODATETIMEOFFSET (@dateTime, '+13:00');  
-- RETURNS 2007-08-28 18:00:30.0000000 +13:00  
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日期和時間資料類型與函式 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

