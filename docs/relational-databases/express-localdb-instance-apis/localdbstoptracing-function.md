---
title: LocalDBStopTracing 函數 |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LocalDBStopTracing
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 1d50e040-8602-4ffa-be8f-b8633fdfa7ff
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b865a7ac9b74f2e17a9897c0178ecb9f48a451b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="localdbstoptracing-function"></a>LocalDBStopTracing 函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  針對目前 Windows 使用者擁有的所有 SQL Server Express LocalDB 執行個體停用 API 呼叫的追蹤。  
  
 **標頭檔：** sqlncli.h  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT LocalDBStopTracing();  
```  
  
## <a name="returns"></a>傳回值  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外的錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="remarks"></a>備註  
 如需使用 LocalDB API 的程式碼範例，請參閱[SQL Server Express LocalDB 參考](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
