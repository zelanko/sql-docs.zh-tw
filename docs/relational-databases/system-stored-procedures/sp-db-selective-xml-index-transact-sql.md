---
description: sp_db_selective_xml_index (Transact-SQL)
title: sp_db_selective_xml_index (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 787750b0b69f70989d6a060f82e754573189d708
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481398"
---
# <a name="sp_db_selective_xml_index-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  啟用和停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫上的選擇性 XML 索引功能。 如果呼叫時未使用任何參數，則預存程序會在特定資料庫上啟用選擇性 XML 索引時傳回 1。  
  
> [!NOTE]  
>  若要使用這個預存程式停用選擇性 XML 索引，必須使用 [ALTER database SET Options &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 命令，將資料庫設為簡單復原模式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>引數  
`[ @ db_name = ] 'db_name'` 要啟用或停用選擇性 XML 索引之資料庫的名稱。 如果 *db_name* 為 Null，則會假設為目前的資料庫。  
  
`[ @action = ] 'action'` 決定是否要啟用或停用索引。 如果傳遞的另一個值是 ' on '、' true '、' off ' 或 ' false ' 以外的值，則會引發錯誤。  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 如果在特定資料庫上啟用選擇性 XML 索引，則為**1** 。  
  
## <a name="examples"></a>範例  
  
### <a name="a-enable-selective-xml-index-functionality"></a>A. 啟用選擇性 XML 索引功能  
 下列範例會在目前資料庫上啟用選擇性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'on';  
GO  
```  
  
 下列範例會在 AdventureWorks2012 資料庫上啟用選擇性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'true';  
GO  
```  
  
### <a name="b-disable-selective-xml-index-functionality"></a>B. 停用選擇性 XML 索引功能  
 下列範例會在目前資料庫上停用選擇性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'off';  
GO  
```  
  
 下列範例會在 AdventureWorks2012 資料庫上停用選擇性 XML 索引。  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'false';  
GO  
```  
  
### <a name="c-detect-if-selective-xml-index-is-enabled"></a>C. 偵測選擇性 XML 索引是否已啟用  
 下列範例會偵測選擇性 XML 索引是否已啟用。 如果選擇性 XML 索引已啟用，則傳回 1。  
  
```  
EXECUTE sys.sp_db_selective_xml_index;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [選擇性 XML 索引 &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
