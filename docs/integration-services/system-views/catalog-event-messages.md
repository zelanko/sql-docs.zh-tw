---
title: catalog.event_messages | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a31a654f-31e9-4da1-aabf-182b07848e36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e19ca7fac23979ecd691ed6cab45fa2cfec9564
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912626"
---
# <a name="catalogevent_messages"></a>catalog.event_messages 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示作業期間所記錄的訊息資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|Event_message_ID|BIGINT|事件訊息的唯一識別碼。|  
|Operation_id|BIGINT|作業的類型。<br /><br /> 如需作業類型的清單，請參閱 [catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)。|  
|Message_time|datetimeoffset(7)|建立訊息的時間。|  
|Message_type|SMALLINT|顯示的訊息類型。 如需訊息類型的詳細資訊，請參閱 [catalog.operation_messages &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)。|  
|Message_source_type|SMALLINT|訊息的來源。|  
|message|nvarchar(max)|訊息的文字。|  
|Extended_info_id|BIGINT|在 [catalog.extended_operation_info &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) 檢視中所找到，且與作業訊息相關之其他資訊的識別碼。|  
|Package_name|nvarchar(260)|封裝檔案的名稱。|  
|Event_name|nvarchar(1024)|與訊息相關聯的執行階段事件。|  
|Message_source_name|nvarchar(4000)|訊息來源的封裝元件。|  
|Message_source_id|nvarchar(38)|訊息來源的唯一識別碼。|  
|Subcomponent_name|nvarchar(4000)|訊息來源的資料流程元件。<br /><br /> [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 引擎傳回訊息時，SSIS.Pipeline 會出現在這個資料行中。|  
|Package_path|nvarchar(max)|封裝中元件的唯一路徑。|  
|Execution_path|nvarchar(max)|從父封裝到元件執行點的完整路徑。<br /><br /> 此路徑也會擷取元件的反覆運算。|  
|threadID|int|記錄訊息時執行之執行緒的識別碼。|  
|Message_code|int|與訊息相關聯的代碼。|  
  
## <a name="remarks"></a>備註  
 這個檢視會顯示下列訊息來源類型。  
  
|**message_source_type**|描述|  
|-------------------------------|-----------------|  
|10|項目 API，例如 T-SQL 和 CLR 預存程序|  
|20|用來執行封裝的外部處理序 (ISServerExec.exe)|  
|30|封裝層級物件|  
|40|控制流程工作|  
|50|控制流程容器|  
|60|資料流程工作|  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   作業的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格。  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
  
