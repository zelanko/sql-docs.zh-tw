---
title: DROP EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a86e48453b8d4d64a2f22fa84293a65554a8cf82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723216"
---
# <a name="drop-external-data-source-transact-sql"></a>DROP EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  移除 PolyBase 外部資料來源。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *external_data_source_name*  
 要卸除之外部資料來源的名稱。  
  
## <a name="metadata"></a>中繼資料  
 若要檢視外部資料來源的清單，請使用 sys.external_data_sources 系統檢視。  
  
```  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>[權限]  
 需要 ALTER ANY EXTERNAL DATA SOURCE。  
  
## <a name="locking"></a>鎖定  
 在外部資料來源物件上採取共用鎖定。  
  
## <a name="general-remarks"></a>一般備註  
 卸除外部資料來源並不會移除外部資料。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-basic-syntax"></a>A. 使用基本語法  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

