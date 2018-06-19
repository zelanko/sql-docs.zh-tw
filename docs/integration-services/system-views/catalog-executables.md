---
title: catalog.executables | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 66f3e926072e79fbe18774cc3f9ab300a91d7ba5
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35329162"
---
# <a name="catalogexecutables"></a>catalog.executables
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  這個檢視會針對指定之執行中的每個可執行檔顯示一個資料列。  
  
 可執行檔是您加入至封裝之控制流程的工作或容器。  
  
|資料行名稱|**Data type**|描述|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|可執行檔的唯一識別碼。|  
|execution_id|**bigint**|執行之執行個體的唯一識別碼。|  
|executable_name|**nvarchar(4000)**|可執行檔的名稱。|  
|executable_guid|**nvarchar(38)**|可執行檔的 GUID。|  
|package_name|**nvarchar(260)**|封裝名稱。|  
|package_path|**nvarchar(max)**|封裝的路徑。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   執行的執行個體之 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
## <a name="remarks"></a>Remarks  
  
