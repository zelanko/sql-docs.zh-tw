---
title: 建立擴充的事件工作階段 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 34b1e95a-a80e-4aca-9201-abde47f2ca74
caps.latest.revision: 4
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: db38720b01cf8e851dfb3f047f37701381a613d7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035277"
---
# <a name="create-an-extended-events-session"></a>建立擴充事件工作階段
  您可以使用查詢編輯器來建立擴充事件工作階段，也可以在物件總管中建立工作階段。 在物件總管中，擴充事件提供了兩個可用來建立、修改和檢視事件工作階段資料的使用者介面：指引您完成事件工作階段建立程序的精靈，以及提供了更多進階組態選項的新增工作階段 UI。 您可以建立擴充事件工作階段來診斷 SQL Server 追蹤，以便解決下列問題：  
  
-   尋找最費時的查詢  
  
-   尋找導致閂鎖競爭的根本原因  
  
-   尋找封鎖其他查詢的查詢  
  
-   疑難排解因重新編譯查詢所致的過度使用 CPU 的問題  
  
-   疑難排解死結  
  
## <a name="in-this-section"></a>本節內容  
 [使用查詢編輯器建立擴充事件工作階段](../../2014/database-engine/create-an-extended-events-session-using-query-editor.md)  
  
 [建立擴充的事件工作階段使用精靈&#40;物件總管&#41;](../ssms/object/object-explorer.md)  
  
 [建立擴充的事件工作階段使用新的工作階段 對話方塊](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)  
  
  