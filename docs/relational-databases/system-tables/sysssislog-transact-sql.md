---
title: g (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
caps.latest.revision: 40
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0f60ec3735bc89c7e729ac6ec01e6f62f126c51f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261174"
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對封裝或它們的工作和容器在執行階段所產生的每個記錄項目，各包含一個資料列。 當您安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 時，會在 msdb 資料庫中建立這份資料表。 如果您將記錄工作設定成記錄到不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中，就會在指定的資料庫中建立這種格式的 sysssislog 資料表。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 下表中寫入記錄項目**只**當封裝使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄提供者。  
  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|記錄項目的唯一識別碼。|  
|event|**sysname**|產生記錄項目的事件名稱。|  
|computer|**nvarchar**|產生記錄項目時，封裝執行所在的電腦。|  
|! 運算子之後|**nvarchar**|產生記錄項目的封裝之執行者的使用者名稱。|  
|來源|**nvarchar**|此封裝內產生記錄項目的可執行檔名稱。|  
|sourceid|**uniqueidentifier**|此封裝內產生記錄項目之可執行檔的 GUID。|  
|executionid|**uniqueidentifier**|產生記錄項目之可執行檔執行個體的 GUID。|  
|starttime|**datetime**|封裝開始執行的時間。|  
|endtime|**datetime**|封裝完成的時間。<br /><br /> 系統不會實作這個功能。 endtime 資料行中的值永遠與 starttime 資料行中的值相同。|  
|datacode|**int**|選擇性的整數值，一般會指示容器或工作的執行結果。|  
|databytes|**image**|包含其他資訊的選擇性位元組陣列。|  
|message|**nvarchar**|事件的描述以及與此事件相關的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services & #40;SSIS & #41;記錄](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
