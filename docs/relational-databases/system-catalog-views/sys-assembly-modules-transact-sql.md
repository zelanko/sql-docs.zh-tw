---
description: sys.assembly_modules (Transact-SQL)
title: sys. assembly_modules (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e8d04bb98a27ea81f2624c5d9e822b254eee9503
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464830"
---
# <a name="sysassembly_modules-transact-sql"></a>sys.assembly_modules (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  針對由 Common Language Runtime (CLR) 組件定義的每個函數、程序或觸發程序，各傳回一個資料列。 這個目錄檢視會將 CLR 預存程序、CLR 觸發程序或 CLR 函數對應至它們的基本實作。 TA、AF、PC、FS 和 FT 類型的物件，各有相關聯的組件模組。 若要找出物件與組件之間的關聯，可以將這個目錄檢視合併到其他目錄檢視。 例如，當您建立 CLR 預存程式時，它會以 **sys. objects**中的一個資料清單示、 **sys. 程式** 中的一個資料列， (繼承自 **sys.databases**) ，以及 **sys. assembly_modules**中的一個資料列。 預存程式本身是以 **sys. objects** 和 **sys. 程式**中的中繼資料來表示。 在 **sys. assembly_modules**中，可以找到程式基礎 CLR 實作為的參考。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|SQL 物件的物件識別碼。 在資料庫中，這是唯一的。|  
|**assembly_id**|**int**|建立這個模組所用之組件的識別碼。|  
|**assembly_class**|**sysname**|定義這個模組之組件內的類別名稱。|  
|**assembly_method**|**sysname**|定義此模組的 **assembly_class** 內的方法名稱。<br /><br /> 如果是彙總函式 (AF)，則為 NULL。|  
|**null_on_null_input**|**bit**|模組宣告的目的不是為了因應任何 NULL 輸入而產生 NULL 輸出。|  
|**execute_as_principal_id**|**int**|執行內容所用的資料庫主體識別碼，由 CLR 函數、預存程序或觸發程序的 EXECUTE AS 子句所指定。<br /><br /> NULL = EXECUTE AS CALLER。 這是預設值。<br /><br /> 指定之資料庫主體的識別碼 = EXECUTE AS SELF、EXECUTE AS *user_name*或 execute as *login_name*。<br /><br /> -2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
