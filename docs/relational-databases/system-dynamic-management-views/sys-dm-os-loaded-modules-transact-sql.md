---
title: sys.databases dm_os_loaded_modules （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_loaded_modules
- dm_os_loaded_modules
- sys.dm_os_loaded_modules_TSQL
- dm_os_loaded_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_loaded_modules dynamic management view
ms.assetid: 56c7743a-b568-4943-bd3b-73c57d9d641c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 58f0258843995acc82e84d69a4d2d101594fc313
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820804"
---
# <a name="sysdm_os_loaded_modules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對已載入至伺服器位址空間的每一個模組，各傳回一個資料列。  
  
> [!NOTE]  
>  若要從呼叫此 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，請使用**dm_pdw_nodes_os_loaded_modules**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary(8)**|處理序中的模組位址。|  
|**file_version**|**Varchar （23）**|檔案的版本。 以下列格式呈現：<br /><br /> x.x:x.x|  
|**product_version**|**Varchar （23）**|產品的版本。 以下列格式呈現：<br /><br /> x.x:x.x|  
|**debug.exe**|**bit**|1 = 模組是已載入模組的偵錯版本。|  
|**patched**|**bit**|1 = 模組已修補。|  
|**版**|**bit**|1 = 模組是已載入模組的發行前版本。|  
|**private_build**|**bit**|1 = 模組是已載入模組的私用建置。|  
|**special_build**|**bit**|1 = 模組是已載入模組的特殊建置。|  
|**語言**|**int**|模組之版本資訊的語言。|  
|**company**|**nvarchar(256)**|建立模組的公司名稱。|  
|**描述**|**nvarchar(256)**|模組的描述。|  
|**name**|**nvarchar(255)**|模組的名稱。 包含模組的完整路徑。|  
|**pdw_node_id**|**int**|**適用於**：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
