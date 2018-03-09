---
title: catalog.execution_data_taps | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 15486c5dcdce5fc3e3f67ed4aec977d1eb3f4ede
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="catalogexecutiondatataps"></a>catalog.execution_data_taps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示執行中定義之每個資料點選的資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|資料點選的唯一識別碼 (ID)。|  
|execution_id|**bigint**|執行之執行個體的唯一識別碼 (ID)。|  
|package_path|**nvarchar(max)**|點選資料之資料流程工作的封裝路徑。|  
|dataflow_path_id_string|**nvarchar(4000)**|資料流程路徑的識別字串。|  
|dataflow_task_guid|**uniqueidentifier**|資料流程工作的唯一識別碼 (ID)。|  
|max_rows|**int**|要擷取的資料列數。 如果沒有指定此值，則會擷取所有資料列。|  
|filename|**nvarchar(4000)**|資料傾印檔案的名稱。 如需相關資訊，請參閱 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   執行的執行個體之 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
## <a name="see-also"></a>另請參閱  
 [產生套件執行的傾印檔案](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
