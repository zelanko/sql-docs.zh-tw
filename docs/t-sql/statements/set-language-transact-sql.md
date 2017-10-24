---
title: "設定語言 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_LANGUAGE_TSQL
- SET LANGUAGE
dev_langs:
- TSQL
helpviewer_keywords:
- LANGUAGE option
- languages [SQL Server], setting language
- SET LANGUAGE statement
- options [SQL Server], date
- default languages
ms.assetid: 0ec0e5cf-e115-4be9-a0db-e65837d6fa45
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f334049b696685b366c36484857d1340853a4b15
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-language-transact-sql"></a>SET LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  指定工作階段的語言環境。 工作階段語言決定**datetime**格式和系統訊息。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET LANGUAGE { [ N ] 'language' | @language_var }   
```  
  
## <a name="arguments"></a>引數  
 [**N**]**'***語言***'**  |   **@**  *language_var*  
 語言的名稱是存放在[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)。 這個引數可以是 Unicode 或轉換成 Unicode 的 DBCS。 若要以 Unicode 指定語言，使用**N'***語言***'**。 如果指定的變數，變數必須是**sysname**。  
  
## <a name="remarks"></a>備註  
 SET LANGUAGE 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 SET LANGUAGE 會隱含地設定的設定[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會將預設語言設為 `Italian`，顯示月份名稱，再切換回 `us_english` 並重新顯示月份名稱。  
  
```  
DECLARE @Today DATETIME;  
SET @Today = '12/5/2007';  
  
SET LANGUAGE Italian;  
SELECT DATENAME(month, @Today) AS 'Month Name';  
  
SET LANGUAGE us_english;  
SELECT DATENAME(month, @Today) AS 'Month Name' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [sp_helplanguage &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

