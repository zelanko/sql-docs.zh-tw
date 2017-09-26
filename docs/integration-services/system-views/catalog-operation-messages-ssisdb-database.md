---
title: "catalog.operation_messages （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 235e9896cbf075bdc26e3df120b23091b8e82d6d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogoperationmessages-ssisdb-database"></a>catalog.operation_messages (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中之作業期間所記錄的訊息。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|訊息的唯一識別碼 (ID)。|  
|operation_id|**bigint**|作業的唯一識別碼。|  
|message_time|**datetimeoffset(7)**|建立訊息的日期和時間。|  
|m|**smallint**|顯示的訊息類型。|  
|message_source_type|**smallint**|訊息來源類型的識別碼。|  
|message|**nvarchar(max)**|訊息的文字。|  
|extended_info_id|**bigint**|在中找到的其他相關資訊的作業訊息，ID [x](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)檢視。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示在目錄作業期間所記錄之每個訊息的資料列。 訊息可由伺服器、封裝執行處理或執行引擎所產生。  
  
 這個檢視會顯示下列訊息類型：  
  
|**m**值|Description|  
|-----------------------------|-----------------|  
|-1|Unknown|  
|120|錯誤|  
|110|警告|  
|70|資訊|  
|10|驗證前|  
|20|驗證後|  
|30|執行前|  
|40|執行後|  
|60|進度|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|Diagnostic|  
|200|Custom|  
|140|DiagnosticEx<br /><br /> 只要執行封裝工作執行子封裝，它就會記錄這個事件。 事件訊息是由傳遞至子封裝的參數值所組成。<br /><br /> DiagnosticEx 之訊息資料行的值是 XML 文字。|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
 這個檢視會顯示下列訊息來源類型。  
  
|**message_source_type**|Description|  
|-------------------------------|-----------------|  
|10|項目 API，例如 T-SQL 和 CLR 預存程序|  
|20|用來執行封裝的外部處理序 (ISServerExec.exe)|  
|30|封裝層級物件|  
|40|控制流程工作|  
|50|控制流程容器|  
|60|資料流程工作|  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   作業的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
> [!NOTE]  
>  當您擁有在伺服器上執行操作的權限時，也會具有檢視作業資訊的權限。 強制使用資料列層級安全性，只會顯示您具有檢視權限的資料列。  
  
  
