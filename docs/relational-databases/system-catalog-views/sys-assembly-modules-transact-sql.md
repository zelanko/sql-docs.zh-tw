---
title: sys.assembly_modules (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ade1adbfeb8292e894ce18db305687c7092707cf
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391444"
---
# <a name="sysassemblymodules-transact-sql"></a>sys.assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  針對由 Common Language Runtime (CLR) 組件定義的每個函數、程序或觸發程序，各傳回一個資料列。 這個目錄檢視會將 CLR 預存程序、CLR 觸發程序或 CLR 函數對應至它們的基本實作。 TA、AF、PC、FS 和 FT 類型的物件，各有相關聯的組件模組。 若要找出物件與組件之間的關聯，可以將這個目錄檢視合併到其他目錄檢視。 比方說，當您建立 CLR 預存程序時，它由一個資料列**sys.objects**，下列其中一個資料列中**sys.procedures** (該項則繼承自**sys.objects**)，和中的資料列**sys.assembly_modules**。 中的中繼資料表示的預存程序本身**sys.objects**並**sys.procedures**。 此程序基礎 CLR 實作的參考中找到**sys.assembly_modules**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|SQL 物件的物件識別碼。 在資料庫中，這是唯一的。|  
|**assembly_id**|**int**|建立這個模組所用之組件的識別碼。|  
|**assembly_class**|**sysname**|定義這個模組之組件內的類別名稱。|  
|**assembly_method**|**sysname**|名稱內的方法**assembly_class**定義這個模組。<br /><br /> 如果是彙總函式 (AF)，則為 NULL。|  
|**null_on_null_input**|**bit**|模組宣告的目的不是為了因應任何 NULL 輸入而產生 NULL 輸出。|  
|**execute_as_principal_id**|**int**|執行內容所用的資料庫主體識別碼，由 CLR 函數、預存程序或觸發程序的 EXECUTE AS 子句所指定。<br /><br /> NULL = EXECUTE AS CALLER。 這是預設值。<br /><br /> 指定的資料庫主體識別碼 = EXECUTE AS SELF、 EXECUTE AS *user_name*，或 EXECUTE AS *login_name*。<br /><br /> -2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
