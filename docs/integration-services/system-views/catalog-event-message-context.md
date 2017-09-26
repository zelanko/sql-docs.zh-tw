---
title: "catalog.event_message_context |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 273a54f8-b107-4f36-9461-2b475644760d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b7aeb07c52f7ed00aa5a6a29cdd054258cb62d65
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogeventmessagecontext"></a>catalog.event_message_context
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的執行顯示與執行事件訊息相關聯之條件的詳細資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|Context_id|bigint|錯誤內容的唯一識別碼。|  
|Event_message_id|bigint|與內容相關之訊息的唯一識別碼。|  
|Context_depth|int|隨著深度的增加，內容與錯誤之間的距離越遠。 當發生錯誤時，內容深度從 1 開始。 值為 0 表示開始執行之前的封裝狀態。|  
|Package_path|Nvarchar(max)|內容來源的封裝路徑。|  
|Context_type|smallint|內容來源的物件類型。 請參閱**備註**部分內容類型清單。|  
|Context_source_name|Nvarchar （4000)|內容來源的物件名稱。|  
|Context_source_id|Nvarchar(38)|內容來源之物件的唯一識別碼。|  
|Property_name|Nvarchar （4000)|與內容來源相關聯的屬性名稱。|  
|Property_value|Sql_variant|與內容來源相關聯的屬性值。|  
  
## <a name="remarks"></a>備註  
 下表列出這些內容類型。  
  
||||  
|-|-|-|  
|內容類型值|類型名稱|Description|  
|10|工作|發生錯誤時的工作狀態。|  
|20|管線|錯誤來自管線元件：來源、目的地或轉換元件。|  
|30|序列|數列的狀態。|  
|40|For 迴圈|For 迴圈的狀態。|  
|50|Foreach 迴圈|Foreach 迴圈的狀態|  
|60|封裝|發生錯誤時的封裝狀態。|  
|70|變數|變數值|  
|80|[ODBC 目的地編輯器]|連接管理員的屬性。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視需要下列其中一個權限：  
  
-   作業的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色。  
  
-   成員資格**sysadmin**伺服器角色。  
  
  
