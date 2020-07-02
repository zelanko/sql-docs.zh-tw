---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.parameters_TSQL
- sys.parameters
- parameters
- parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameters catalog view
- table-valued parameters,sys.parameters
ms.assetid: 24e2764b-c8e5-4322-97a4-7407d8b8a92b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 377c3f0c569815dbd348020610a6dddb7f01d745
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760305"
---
# <a name="sysparameters-transact-sql"></a>sys.parameters (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  針對接受參數之物件的每個參數，各包含一個資料列。 如果物件是純量函數，也會有一個描述傳回值的單一資料列。 該資料列的**parameter_id**值為0。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|這個參數所屬物件的識別碼。|  
|**name**|**sysname**|參數的名稱。 在物件中，這是唯一的。<br /><br /> 如果物件是純量函數，參數名稱就是代表傳回值之資料列中的空字串。|  
|**parameter_id**|**int**|參數的識別碼。 在物件中，這是唯一的。<br /><br /> 如果物件是純量函數， **parameter_id** = 0 代表傳回值。|  
|**system_type_id**|**tinyint**|參數系統類型的識別碼。|  
|**user_type_id**|**int**|使用者所定義的參數類型識別碼。<br /><br /> 若要傳回類型的名稱，請在此資料行上加入[sys.databases](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目錄檢視。|  
|**max_length**|**smallint**|參數的最大長度 (以位元組為單位)。<br /><br /> 當資料行資料類型為**Varchar （max）**、 **Nvarchar （max）**、 **Varbinary （max）** 或**xml**時，Value =-1。|  
|**有效位數**|**tinyint**|如果是以數值為基礎，便是參數的有效位數；否則，便是 0。|  
|**scale**|**tinyint**|如果是以數值為基礎，便是參數的小數位數；否則，便是 0。|  
|**is_output**|**bit**|1 = 參數是 OUTPUT 或 RETURN，否則就是 0。|  
|**is_cursor_ref**|**bit**|1 = 參數是一個資料指標參考參數。|  
|**has_default_value**|**bit**|1 = 參數有預設值。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會在此目錄檢視中保留 CLR 物件的預設值；因此，對於 [!INCLUDE[tsql](../../includes/tsql-md.md)] 物件，此資料行的值為 0。 若要在物件中查看參數的預設值 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，請查詢[sys.databases sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目錄檢視的 [**定義**] 資料行，或使用[OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)系統函數。|  
|**is_xml_document**|**bit**|1 = 內容是完整的 XML 文件集。<br /><br /> 0 = 內容是檔片段，或者資料行的資料類型不是**xml**。|  
|**default_value**|**sql_variant**|如果**has_default_value**是1，這個資料行的值就是參數的預設值。否則為 Null。|  
|**xml_collection_id**|**int**|如果參數的資料類型是**xml** ，而且 xml 為類型，則為非零。 這個值是包含參數的驗證 XML 結構描述命名空間之集合的識別碼。<br /><br /> 0 = 沒有 XML 結構描述集合。|  
|**is_readonly**|**bit**|1 = 參數為 READONLY，否則就是 0。|  
|**is_nullable**|**bit**|1 = 參數不可為 Null  (預設值)。<br /><br /> 0 = 參數不可為 Null，適用於原生編譯預存程序更有效率的執行。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [all_parameters &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)   
 [sys.system_parameters &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
