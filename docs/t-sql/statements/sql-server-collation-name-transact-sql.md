---
title: SQL Server 定序名稱 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a59461aa29a524d5d92681bbd1f76889e4239fca
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2018
ms.locfileid: "39451962"
---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 定序名稱 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  這是指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序之定序名稱的單一字串。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 定序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也支援有限數目 (<80) 的定序，稱為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序，這些定序是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 定序之前開發。 為了回溯相容性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序仍然受到支援，但是不應該用於新的開發工作。 如需 Windows 定序的詳細資訊，請參閱 [Windows 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)。  
  
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
  
 **Pref**  
 指定預設為大寫。 即使比較不區分大小寫，但是當沒有其他區分方式時，字母的大寫版本還是會排在小寫版本的前面。  
  
 *Codepage*  
 指定識別定序所用字碼頁的一至四位數。 **CP1** 指定字碼頁 1252；若是其他所有字碼頁，則必須指定完整的字碼頁編號。 例如，**CP1251** 指定字碼頁 1251，而 **CP850** 則指定字碼頁 850。  
  
 *CaseSensitivity*  
 **CI** 指定不區分大小寫，**CS** 指定區分大小寫。  
  
 *AccentSensitivity*  
 **AI** 指定不區分腔調字，**AS** 指定區分腔調字。  
  
 **BIN**  
 指定要用的二進位排序次序。  
  
## <a name="remarks"></a>Remarks  
 若要列出您的伺服器支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序，請執行下列查詢。  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

>  [!NOTE]  
>  針對排序順序識別碼 80，請使用任何 Window 定序與字碼頁 1250，以及二進位順序。 例如：Albanian_BIN、Croatian_BIN、Czech_BIN、Romanian_BIN、Slovak_BIN、Slovenian_BIN。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [常數 &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
