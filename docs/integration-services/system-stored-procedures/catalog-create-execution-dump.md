---
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f0e8a52152975f84315641030dea314dc4ed7c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  導致執行中的封裝暫停，並建立傾印檔案。 此檔案儲存於 \<磁碟機>:\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps 資料夾。  
  
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
 無  
  
## <a name="permissions"></a>Permissions  
 此預存程序需要使用者為 **ssis_admin** 資料庫角色的成員。  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   指定的執行識別碼無效。  
  
-   封裝已完成。  
  
-   封裝目前正在建立傾印檔案。  
  
## <a name="see-also"></a>另請參閱  
 [產生套件執行的傾印檔案](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
