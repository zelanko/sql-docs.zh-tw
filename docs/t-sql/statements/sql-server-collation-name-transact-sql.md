---
title: "SQL Server 定序名稱 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7265f4efe0d790ab61e4e522af83d6b91b710a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 定序名稱 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  這是指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序之定序名稱的單一字串。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 定序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也支援有限數目 (<80) 的定序，稱為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序，這些定序是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 定序之前開發。 為了回溯相容性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序仍然受到支援，但是不應該用於新的開發工作。 如需有關 Windows 定序的詳細資訊，請參閱[Windows 定序名稱 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
<SQL_collation_name> :: =   
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>  
  
<ComparisonStyle> ::=  
_CaseSensitivity_AccentSensitivity | _BIN  
```  
  
## <a name="arguments"></a>引數  
 *SortRules*  
 用來識別指定字典排序時套用排序規則之字母或語言的字串。 例如 Latin1_General 或 Polish。  
  
 **喜好設定**  
 指定預設為大寫。 即使比較不區分大小寫，但是當沒有其他區分方式時，字母的大寫版本還是會排在小寫版本的前面。  
  
 *Codepage*  
 指定識別定序所用字碼頁的一至四位數。 **CP1**指定字碼頁 1252年，就會在指定的其他所有字碼都頁的完整的字碼頁編號。 例如， **CP1251**指定字碼頁 1251年和**CP850**指定字碼頁 850。  
  
 *CaseSensitivity*  
 **CI**指定區分大小寫， **CS**指定區分大小寫。  
  
 *AccentSensitivity*  
 **AI**指定不區分腔調字， **AS**指定區分腔調字。  
  
 **分類收納**  
 指定要用的二進位排序次序。  
  
## <a name="remarks"></a>備註  
 若要列出您的伺服器支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序，請執行下列查詢。  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

>  [!NOTE]  
>  排序順序識別碼 80，使用任何 Window 定序與字碼頁 1250，以及二進位順序。 例如：Albanian_BIN、Croatian_BIN、Czech_BIN、Romanian_BIN、Slovak_BIN、Slovenian_BIN。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [常數 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  

