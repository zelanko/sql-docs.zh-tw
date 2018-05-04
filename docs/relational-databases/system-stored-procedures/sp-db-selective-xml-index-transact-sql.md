---
title: sp_db_selective_xml_index (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3c70fcea339f1cb89026c3afed51f3e25d94f707
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spdbselectivexmlindex-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  啟用和停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫上的選擇性 XML 索引功能。 如果呼叫時未使用任何參數，則預存程序會在特定資料庫上啟用選擇性 XML 索引時傳回 1。  
  
> [!NOTE]  
>  若要停用選擇性 XML 索引使用此預存程序，資料庫必須放在簡單復原模式中使用[ALTER DATABASE SET 選項&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)命令。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>引數  
 [ **@ db_name =** ] **'***db_name***'**  
 要啟用或停用選擇性 XML 索引所在的資料庫名稱。 如果*db_name*是 NULL 時，會假設目前的資料庫。  
  
 [  **@action =** ] **'***動作***'**  
 判斷要啟用或停用索引。 如果傳遞 'on'、'true'、'off' 或 'false' 以外的值，則會引發錯誤。  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **1**如果特定的資料庫上啟用選擇性 XML 索引。  
  
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
  
  
