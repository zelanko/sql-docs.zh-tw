---
title: "catalog.create_execution_dump |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b05e1b46845c0a2b5ee47b94dc239d79d4a12a17
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  導致執行中的封裝暫停，並建立傾印檔案。 此檔案儲存於*\<磁碟機 >*: \Program Files\Microsoft SQL Server\130\Shared\ErrorDumps 資料夾。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id =] *execution_id*  
 執行中之封裝的執行識別碼。 *Execution_id*是**bigint**。  
  
## <a name="example"></a>範例  
 在下列範例中，會提示執行識別碼為 88 的執行中封裝建立傾印檔案。  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要使用者為成員的**ssis_admin**資料庫角色。  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   指定的執行識別碼無效。  
  
-   封裝已完成。  
  
-   封裝目前正在建立傾印檔案。  
  
## <a name="see-also"></a>另請參閱  
 [產生套件執行的傾印檔案](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  

