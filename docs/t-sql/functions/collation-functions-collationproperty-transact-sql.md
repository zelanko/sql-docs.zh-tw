---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d1c121184b4d2af48a547b06fec38b89fa2335da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="collation-functions---collationproperty-transact-sql"></a>定序函式 - COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函式會傳回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中所指定定序的屬性。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>引數  
*collation_name*  
定序的名稱。 *collation_name* 引數具有 **nvarchar(128)** 資料類型，而且沒有預設值。
  
*property*  
定序屬性。 *property* 引數具有 **varchar(128)** 資料類型，而且可以有下列任何一個值：
  
|屬性名稱|描述|  
|---|---|
|**CodePage**|定序的非 Unicode 字碼頁。 請參閱 [Appendix G DBCS/Unicode Mapping Tables](https://msdn.microsoft.com/en-us/library/cc194886.aspx) (附錄 G DBCS/Unicode 對應資料表) 和 [Appendix H Code Pages](https://msdn.microsoft.com/en-us/library/cc195051.aspx) (附錄 H 字碼頁) 來翻譯這些值，以及查看其字元對應。|  
|**LCID**|定序的 Windows LCID。 請參閱 [LCID Structure](https://msdn.microsoft.com/en-us/library/cc233968.aspx) (LCID 結構)，以翻譯這些值 (您必須先轉換成 **varbinary**)。|  
|**ComparisonStyle**|Windows 的定序比較樣式。 針對所有二進位定序，以及所有屬性都區分大小寫時，傳回 0 ((\_BIN) 和 (\_BIN2))。 位元遮罩值：<br /><br /> 忽略大小寫：1<br /><br /> 忽略腔調字：2<br /><br /> 忽略假名：65536<br /><br /> 忽略寬度：131072<br /><br /> 注意：variation-selector-sensitive (\_VSS) 選項仍不會在此值中表示，即使它會影響比較行為也是一樣。|  
|**版本(Version)**|定序的版本，衍生自定序識別碼版本欄位。 傳回 0 到 3 之間的整數值。<br /><br /> 名稱含有 "140" 的定序) 都會傳回 3。<br /><br /> 名稱含有 "100" 的定序) 都會傳回 2。<br /><br /> 名稱含有 "90" 的定序) 都會傳回 1。<br /><br /> 所有其他定序都會傳回 0。|  
  
## <a name="return-types"></a>傳回類型
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
  
  

