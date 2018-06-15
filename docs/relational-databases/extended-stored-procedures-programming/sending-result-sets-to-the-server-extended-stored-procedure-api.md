---
title: 傳送到伺服器 （擴充預存程序 API） 的結果集 |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f9ce579eea9d130110289cb039ebb617d7b89a67
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32935703"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>將結果集傳送到伺服器 (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳送結果集時[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，擴充預存程序應該呼叫適當的 API，如下所示：  
  
-   **Srv_sendmsg**之前或之後與已傳送所有資料列 （如果有的話），可能依任何順序呼叫函式**srv_sendrow**。 所有訊息必須都傳送至用戶端，以都傳送完成狀態之前**srv_senddone**。  
  
-   系統會針對傳送到用戶端的每個資料列，呼叫 **srv_sendrow** 函式一次。 所有資料列必須只能傳送到用戶端之前任何訊息、 狀態值或完成狀態才會傳送**srv_sendmsg**、 **srv_status**引數的**srv_pfield**，或**srv_senddone**。  
  
-   未定義的所有資料行的資料列傳送**srv_describe**導致應用程式引發參考用錯誤訊息，並傳回給用戶端失敗。 在此情況下，不會傳送資料列。  
  
## <a name="see-also"></a>另請參閱  
 [建立擴充預存程序](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
