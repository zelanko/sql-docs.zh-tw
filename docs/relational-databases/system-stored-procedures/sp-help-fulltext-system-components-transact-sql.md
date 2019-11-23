---
title: sp_help_fulltext_system_components （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_components_TSQL
- sp_help_fulltext_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_system_components
ms.assetid: ac1fc7a0-7f46-4a12-8c5c-8d378226a8ce
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98e360887d63db59e1e61bf5c52928e9626b0f39
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304890"
---
# <a name="sp_help_fulltext_system_components-transact-sql"></a>sp_help_fulltext_system_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  傳回有關已註冊之斷詞工具、篩選和通訊協定處理常式的詳細資訊。 **sp_help_fulltext_system_components**也會傳回資料庫識別碼的清單，以及已使用指定之元件的全文檢索目錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_system_components   
         { 'all'| [ @component_type = ] 'component_type' }  
    , [ @param = ] 'param'  
```  
  
## <a name="arguments"></a>引數  
 'all'  
 傳回所有全文檢索元件的資訊。  
  
`[ @component_type = ] component_type` 指定元件的類型。 *component_type*可以是下列其中一項：  
  
-   **系統**  
  
-   **filter**  
  
-   **通訊協定處理常式**  
  
-   **fullpath**  
  
 如果指定了完整路徑，則*param*也必須以元件 DLL 的完整路徑來指定，否則會傳回錯誤訊息。  
  
`[ @param = ] param` 視元件類型而定，這是下列其中一項：地區設定識別碼（LCID）、具有 "." 前置詞的副檔名、通訊協定處理常式的完整元件名稱，或元件 DLL 的完整路徑。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 傳回系統元件的下列結果集。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**componenttype**|**sysname**|這是元件的類型， 它有下列幾種：<br /><br /> filter<br /><br /> protocol handler<br /><br /> wordbreaker|  
|**componentname**|**sysname**|元件的名稱。|  
|**clsid**|**ssNoversion**|元件的類別識別碼。|  
|**fullpath**|**nvarchar(256)**|元件位置的路徑。<br /><br /> Null = 呼叫端不是**serveradmin**固定伺服器角色的成員。|  
|**version**|**nvarchar(30)**|元件的版本。|  
|**負責**|**sysname**|元件的製造商名稱。|  
  
 只有在有一或多個使用*component_type*的全文檢索目錄存在時，才會傳回下列結果集。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**dbid**|**int**|資料庫的識別碼。|  
|**ftcatid**|**int**|全文檢索目錄的識別碼。|  
  
## <a name="permissions"></a>Permissions  
 需要**public**角色中的成員資格;不過，使用者只能看到他們具有 VIEW DEFINITION 許可權之全文檢索目錄的相關資訊。 只有**serveradmin**固定伺服器角色的成員，才能夠看到**fullpath**資料行中的值。  
  
## <a name="remarks"></a>Remarks  
 當準備升級時，這個方法尤其重要。 請在特定資料庫內執行這個預存程序，並利用輸出來判斷升級是否會影響到特定的目錄。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-full-text-system-components"></a>A. 列出所有全文檢索系統元件  
 下列範例會列出已經在伺服器執行個體上註冊的所有全文檢索系統元件。  
  
```  
EXEC sp_help_fulltext_system_components 'all';  
GO  
```  
  
### <a name="b-listing-word-breakers"></a>b. 列出斷詞工具  
 下列範例會列出服務執行個體上所註冊的所有斷詞工具。  
  
```  
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```  
  
### <a name="c-determining-whether-a-specific-word-breaker-is-registered"></a>C. 判斷特定的斷詞工具是否已註冊  
 下列範例會列出土耳其文 (LCID = 1055) 的斷詞工具 (如果它已經安裝在系統上，並在服務執行個體上註冊)。 這個範例會指定參數名稱、 **\@component_type**和 **\@參數**。  
  
```  
EXEC sp_help_fulltext_system_components @component_type = 'wordbreaker', @param = 1055;  
GO  
```  
  
 根據預設，不會安裝這個斷詞工具，所以結果集是空的。  
  
### <a name="d-determining-whether-a-specific-filter-has-been-registered"></a>D. 判斷特定的篩選是否已註冊  
 下列範例會列出 .xdoc 元件的篩選 (如果已經手動將它安裝在系統上，並在伺服器執行個體上註冊它)。  
  
```  
EXEC sp_help_fulltext_system_components 'filter', '.xdoc';  
GO  
```  
  
 根據預設，不會安裝這個篩選，所以結果集是空的。  
  
### <a name="e-listing-a-specific-dll-file"></a>E. 列出特定的 .dll 檔案  
 `nlhtml.dll`下列範例會列出特定的 .dll 檔 {2}，預設情況下會安裝這個檔案。{3}  
  
```  
EXEC sp_help_fulltext_system_components 'fullpath',   
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\nlhtml.dll';  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [查看或變更已註冊的篩選與斷詞](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)工具   
 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [全文檢索搜尋和語義搜尋預存程式&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
