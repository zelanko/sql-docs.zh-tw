---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f47c45f892618120b06a17f45f5d3155e092987a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="collation-functions---collationproperty-transact-sql"></a>定序函式 - COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中所指定定序的屬性。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>引數  
*collation_name*  
這是定序的名稱。 *collation_name* 為沒有預設值的 **nvarchar(128)**。
  
*property*  
這是定序的屬性。 *property* 為 **varchar(128)**，可以是下列值中的任何一個：
  
|屬性名稱|描述|  
|---|---|
|**CodePage**|定序的非 Unicode 字碼頁。 請參閱 [Appendix G DBCS/Unicode Mapping Tables](https://msdn.microsoft.com/en-us/library/cc194886.aspx) (附錄 G DBCS/Unicode 對應資料表) 及 [Appendix H Code Pages](https://msdn.microsoft.com/en-us/library/cc195051.aspx) (附錄 H 字碼頁)，以翻譯這些值並查看他們的字元對應。|  
|**LCID**|定序的 Windows LCID。 請參閱 [LCID Structure](https://msdn.microsoft.com/en-us/library/cc233968.aspx) (LCID 結構)，以翻譯這些值 (您必須先轉換成 **varbinary**)。|  
|**ComparisonStyle**|Windows 的定序比較樣式。 針對所有二進位定序傳回 0，包括 (\_BIN) 和 (\_BIN2)，以及當所有屬性都區分時。 位元遮罩值：<br /><br /> 忽略大小寫：1<br /><br /> 忽略腔調字：2<br /><br /> 忽略假名：65536<br /><br /> 忽略寬度：131072<br /><br /> 注意：即使它會影響比較行為，variation-selector-sensitive (\_VSS) 選項仍不會在此值中表示。|  
|**版本(Version)**|定序的版本，衍生自定序識別碼的版本欄位。 傳回 0 到 3 之間的整數值。<br /><br /> 名稱含有 "140" 的定序) 都會傳回 3。<br /><br /> 名稱含有 "100" 的定序) 都會傳回 2。<br /><br /> 名稱含有 "90" 的定序) 都會傳回 1。<br /><br /> 所有其他定序都會傳回 0。|  
  
## <a name="return-types"></a>傳回型別
**sql_variant**
  
## <a name="examples"></a>範例  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>另請參閱
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

