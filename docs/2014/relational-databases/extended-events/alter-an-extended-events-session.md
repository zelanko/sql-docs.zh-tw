---
title: 更改擴充事件工作階段 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 66108d50898610949cb5cab7fb3bdd2dcc726801
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706793"
---
# <a name="alter-an-extended-events-session"></a>更改擴充事件工作階段
  在您建立「擴充事件」工作階段之後，可以根據您的需求使用 **[SQL Server 擴充事件精靈]** 加以更改。  
  
## <a name="before-you-begin"></a>開始之前  
 您不能更改使用中和非使用中工作階段的目標，而且不能更改使用中工作階段的進階屬性組態。  
  
 您可以對使用中和非使用中的事件工作階段進行以下更改：  
  
-   從工作階段加入或移除事件及更改事件組態，例如事件欄位、篩選和動作。  
  
-   從事件工作階段加入或移除目標。  
  
-   啟用 **[在伺服器啟動時啟動事件工作階段]** 選項。  
  
 您可以對非使用中的事件工作階段進行以下的額外更改：  
  
-   啟用 **[追蹤事件之間的關聯性]** 選項。  
  
-   變更進階屬性組態。  
  
> [!NOTE]  
>  [SQL Server 擴充事件精靈]**** 不支援修改事件工作階段。  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>如何使用 SQL Server 擴充事件精靈更改擴充事件工作階段  
  
-   在物件總管中，依序展開 **[管理]**、 **[擴充事件]** 和 **[工作階段]**。  
  
-   以滑鼠右鍵按一下您要改變的工作階段，然後按一下 [屬性]****。  
  
-   在 **[屬性]** 對話方塊中，進行適當的變更，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER EVENT SESSION &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [使用查詢編輯器建立擴充事件工作階段](../../database-engine/create-an-extended-events-session-using-query-editor.md)  
  
  
