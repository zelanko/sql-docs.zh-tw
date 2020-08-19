---
description: catalog.event_message_context
title: catalog.event_message_context | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 273a54f8-b107-4f36-9461-2b475644760d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e8728d1ddbc8ae7643d0ee660266357d42125c89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495296"
---
# <a name="catalogevent_message_context"></a>catalog.event_message_context 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的執行顯示與執行事件訊息相關聯之條件的詳細資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|Context_id|BIGINT|錯誤內容的唯一識別碼。|  
|Event_message_id|BIGINT|與內容相關之訊息的唯一識別碼。|  
|Context_depth|int|隨著深度的增加，內容與錯誤之間的距離越遠。 當發生錯誤時，內容深度從 1 開始。 值為 0 表示開始執行之前的封裝狀態。|  
|Package_path|Nvarchar(max)|內容來源的封裝路徑。|  
|Context_type|SMALLINT|內容來源的物件類型。 如需內容類型的清單，請參閱＜**備註**＞一節。|  
|Context_source_name|Nvarchar(4000)|內容來源的物件名稱。|  
|Context_source_id|Nvarchar(38)|內容來源之物件的唯一識別碼。|  
|Property_name|Nvarchar(4000)|與內容來源相關聯的屬性名稱。|  
|Property_value|Sql_variant|與內容來源相關聯的屬性值。|  
  
## <a name="remarks"></a>備註  
 下表列出這些內容類型。  
  
|內容類型值|類型名稱|描述|  
|-|-|-|  
|10|Task|發生錯誤時的工作狀態。|  
|20|管線|錯誤來自管線元件：來源、目的地或轉換元件。|  
|30|順序|數列的狀態。|  
|40|For 迴圈|For 迴圈的狀態。|  
|50|Foreach 迴圈|Foreach 迴圈的狀態|  
|60|套件|發生錯誤時的封裝狀態。|  
|70|變數|變數值|  
|80|[ODBC 來源編輯器]|連接管理員的屬性。|  
  
## <a name="permissions"></a>權限  
 這個檢視需要下列其中一個權限：  
  
-   作業的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格。  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
  
