---
title: "WMI Provider for Server Events 類別和屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3c95065d739f30ab1aef09e1e1ed4795ba627e4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>伺服器事件類別和屬性的 WMI 提供者
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]下列伺服器事件組成的程式設計模型的 WMI 提供者伺服器事件。 有兩個主要類別目錄的事件，可以針對提供者發出 WQL 查詢來查詢這些事件。 這些是資料定義語言 (DDL) 事件和追蹤事件。 也可以查詢 QUEUE_ACTIVATION 和 BROKER_QUEUE_DISABLED Service Broker 事件。 請注意下列樹狀圖表的內含本質。 例如，DDL_ASSEMBLY_EVENTS 事件包含任何 ALTER_ASSEMBLY、CREATE_ASSEMBLY 和 DROP_ASSEMBLY 事件。 同樣地，TRC_FULL_TEXT 事件包含任何 FT_CRAWL_ABORTED、FT_CRAWL_STARTED 和 FT_CRAWL_STOPPED 事件。 ALL_EVENTS 涵蓋所有 DDL 事件、追蹤事件、QUEUE_ACTIVATION 和 BROKER_QUEUE_DISABLED。  
  
 若要得知可以從事件或事件群組查詢哪些屬性，請參考事件結構描述。 根據預設，事件結構描述會安裝在以下目錄：[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd。  
  
 另外，您可以在發行的事件結構描述參考[http://schemas.microsoft.com/sqlserver](http://go.microsoft.com/fwlink/?linkid=43100)。  
  
 例如，藉由參考 ALTER_DATABASE 事件，您將學習它的父事件為 DDL_SERVER_LEVEL_EVENTS，而其屬性可以**TSQLCommand**和**DatabaseName**。 事件也會繼承內容**SQLInstance**， **PostTime**， **ComputerName**， **SPID**，和**LoginName**. 此事件沒有任何子事件。  
  
> [!NOTE]  
>  執行類似 DDL 作業的系統預存程序也可以引發事件通知。 請測試事件通知以判斷它們對執行之系統預存程序的回應。 例如，CREATE TYPE 陳述式和**sp_addtype**預存程序都會引發在 CREATE_TYPE 事件建立的事件通知。 如需詳細資訊，請參閱[DDL 事件](../../relational-databases/triggers/ddl-events.md)。  
  
 **資料定義語言事件和事件群組**  
  
 ![WMI Provider for Server Events 事件樹](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "WMI Provider for Server Events 事件樹")  
  
 **追蹤事件和事件群組**  
  
 ![追蹤事件和事件群組](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "追蹤事件和事件群組")  
  
## <a name="see-also"></a>請參閱  
 [WMI 事件提供者伺服器概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [搭配伺服器事件的 WMI 提供者使用 WQL](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
