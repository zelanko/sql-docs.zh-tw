---
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a48142752c0016a2c215b9333dcbf518b63179c5
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914098"
---
# <a name="catalogcreate_execution_dump"></a>catalog.create_execution_dump 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  導致執行中的封裝暫停，並建立傾印檔案。 此檔案會儲存在 *\<drive>* :\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps 資料夾。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id = ] *execution_id*  
 執行中之封裝的執行識別碼。 *execution_id* 是 **bigint**。  
  
## <a name="example"></a>範例  
 在下列範例中，會提示執行識別碼為 88 的執行中封裝建立傾印檔案。  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 此預存程序需要使用者為 **ssis_admin** 資料庫角色的成員。  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   指定的執行識別碼無效。  
  
-   封裝已完成。  
  
-   封裝目前正在建立傾印檔案。  
  
## <a name="see-also"></a>另請參閱  
 [產生套件執行的傾印檔案](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
