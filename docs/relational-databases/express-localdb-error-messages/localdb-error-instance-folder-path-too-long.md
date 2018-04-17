---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 507aeb2773a56128300db99cd8e58517a401a315
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|이벤트 ID|260|  
|이벤트 원본|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|메시지 텍스트|本機資料庫執行個體資料夾的完整路徑長度比 MAX_PATH 還長。 執行個體必須存放在資料夾中： SQL Server 本機 DB\Instances %%LOCALAPPDATA%%\Microsoft\Microsoft\\< 執行個體名稱\>。|  
  
## <a name="explanation"></a>說明  
 應儲存執行個體的路徑長度超過 MAX_PATH。  
  
## <a name="user-action"></a>사용자 동작  
 請建立長度短於 MAX_PATH 的新路徑。  
  
  
