---
title: SESSIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSIONPROPERTY
- SESSIONPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, SESSIONPROPERTY function
- SESSIONPROPERTY function
- sessions [SQL Server], SET options settings
ms.assetid: 1f3730b4-1495-4d3a-af43-e57952812df9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e22d0c36c3a5ce614357566079ec81dc54b7c70e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68022188"
---
# <a name="sessionproperty-transact-sql"></a>SESSIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回工作階段的 SET 選項設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SESSIONPROPERTY (option)  
```  
  
## <a name="arguments"></a>引數  
 *選項*  
 這是此工作階段的目前選項設定。 *option* 可以是下列值之一。  
  
|選項|描述|  
|------------|-----------------|  
|ANSI_NULLS|指定是否對 Null 值套用等於 (=) 和不等於 (<>) 的 ISO 行為。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_PADDING|控制資料行如何儲存比資料行的定義大小還短的值，以及如何儲存字元和二進位資料含有尾端空格的值。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_WARNINGS|指定是否套用引發特定狀況之錯誤訊息或警告的 ISO 標準行為，其中包括除以零和算術溢位。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ARITHABORT|判斷在查詢執行期間，當發生溢位或除以零的錯誤時，是否結束查詢。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|CONCAT_NULL_YIELDS_ NULL|控制是否將串連結果當作 Null 或空字串值來處理。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|NUMERIC_ROUNDABORT|指定在運算式中捨入造成失去有效位數時，所產生的錯誤訊息和警告。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|QUOTED_IDENTIFIER|指定是否遵照如何利用引號來分隔識別碼和常值字串的 ISO 規則。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|\<任何其他字串>|NULL = 輸入無效。|  
  
## <a name="return-types"></a>傳回型別  
 **sql_variant**  
  
## <a name="remarks"></a>備註  
 SET 選項是由組合伺服器層級、資料庫層級和使用者指定選項來表示。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `CONCAT_NULL_YIELDS_NULL` 選項的設定。  
  
```  
SELECT   SESSIONPROPERTY ('CONCAT_NULL_YIELDS_NULL')  
```  
  
## <a name="see-also"></a>另請參閱  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
