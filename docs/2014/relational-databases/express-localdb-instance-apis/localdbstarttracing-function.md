---
title: LocalDBStartTracing 函式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBStartTracing
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: c7b83833-6d2a-4a06-9cb7-42767bed52c6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: aed6261312414d114fdf9ed92b111d44fbb0f93c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050991"
---
# <a name="localdbstarttracing-function"></a>LocalDBStartTracing 函數
  針對目前 Windows 使用者擁有的所有 SQL Server Express LocalDB 執行個體啟用 API 呼叫的追蹤。  
  
 **標頭檔：** sqlncli。h  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT LocalDBStartTracing();  
```  
  
## <a name="returns"></a>傳回  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_XEVENT_FAILED](../express-localdb-error-messages/localdb-error-xevent-failed.md)  
 無法啟動 LocalDB 執行個體 API 內的 XEvent 引擎。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="remarks"></a>備註  
 如需使用 LocalDB API 的程式碼範例，請參閱[SQL Server Express Localdb 參考](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](sql-server-express-localdb-header-and-version-information.md)  
  
  
