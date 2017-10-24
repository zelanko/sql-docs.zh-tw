---
title: "COLLATIONPROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 166a85e5fe33a95cd8a36f221c2a774e4a0a9fb2
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="collation-functions---collationproperty-transact-sql"></a>定序函式-COLLATIONPROPERTY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中所指定定序的屬性。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>引數  
*sys.databases*  
這是定序的名稱。 *sys.databases*是**nvarchar （128)**，沒有預設值。
  
*屬性*  
這是定序的屬性。 *屬性*是**varchar （128)**，而且可以是下列值之一：
  
|屬性名稱|Description|  
|---|---|
|**CodePage**|定序的非 Unicode 字碼頁。 請參閱[附錄 G DBCS/Unicode 對應資料表](https://msdn.microsoft.com/en-us/library/cc194886.aspx)和[附錄 H 字碼頁](https://msdn.microsoft.com/en-us/library/cc195051.aspx)轉譯這些值，並查看其字元對應。|  
|**LCID**|定序的 Windows LCID。 請參閱[LCID 結構](https://msdn.microsoft.com/en-us/library/cc233968.aspx)轉譯這些值 (您必須將轉換成`VARBINARY`第一個)。|  
|**ComparisonStyle**|Windows 的定序比較樣式。 傳回 0 代表所有二進位定序 (兩者`_BIN`和`_BIN2`) 以及當所有屬性都是機密。 位元遮罩值：<br /><br /> 忽略大小寫： 1<br /><br /> 忽略腔調字： 2<br /><br /> 忽略假名： 65536<br /><br /> 忽略寬度： 131072|  
|**版本**|定序的版本，衍生自定序識別碼的版本欄位。 傳回介於 0 到 3 之間的整數值。<br /><br /> 「 140"名稱中使用的定序會傳回 3。<br /><br /> 含有"100"，在名稱中的定序都會傳回 2。<br /><br /> 含有"90"的名稱中的定序都會傳回 1。<br /><br /> 所有其他定序都會傳回 0。|  
  
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
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>另請參閱
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  


