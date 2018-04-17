---
title: sys.fn_helpcollations (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_helpcollations
- fn_helpcollations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_helpcollations function
- collations [SQL Server], supported
- fn_helpcollations function
ms.assetid: b5082e81-1fee-4e2c-b567-5412eaee41c1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0ad1f8d41d4d4ecbbe6fd00f55310a64c4780c9f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysfnhelpcollations-transact-sql"></a>sys.fn_helpcollations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  傳回所有支援的定序清單。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
fn_helpcollations ()  
```  
  
## <a name="tables-returned"></a>傳回的資料表  
 **fn_helpcollations**會傳回下列資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|名稱|**sysname**|標準定序名稱|  
|Description|**nvarchar(1000)**|定序的描述|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 定序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也支援有限數目 (<80) 的定序，稱為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序，這些定序是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 定序之前開發。 為了回溯相容性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序仍然受到支援，但是不應該用於新的開發工作。 如需 Windows 定序的詳細資訊，請參閱 [Windows 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)。 如需有關定序的詳細資訊，請參閱[Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  

## <a name="examples"></a>範例  
 下列範例會傳回開頭是 `L` 字母，而且是二進位排序定序的所有定序名稱。  
  
```  
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name like 'L%' AND Description LIKE '% binary sort';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Name                   Description  
 -------------------    ------------------------------------  
 Lao_100_BIN            Lao-100, binary sort  
 Latin1_General_BIN     Latin1-General, binary sort  
 Latin1_General_100_BIN Latin1-General-100, binary sort  
 Latvian_BIN            Latvian, binary sort  
 Latvian_100_BIN        Latvian-100, binary sort  
 Lithuanian_BIN         Lithuanian, binary sort  
 Lithuanian_100_BIN     Lithuanian-100, binary sort  
  
 (7 row(s) affected)  
 ```    
  
## <a name="see-also"></a>另請參閱  
[COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
[COLLATIONPROPERTY &#40;Transact SQL&#41;](../../t-sql/functions/collation-functions-collationproperty-transact-sql.md)  
[Azure SQL 資料倉儲的資料庫定序支援](https://azure.microsoft.com/blog/database-collation-support-for-azure-sql-data-warehouse-2)  

