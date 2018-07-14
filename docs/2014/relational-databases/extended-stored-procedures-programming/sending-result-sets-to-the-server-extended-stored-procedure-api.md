---
title: 傳送結果集至伺服器 （擴充預存程序 API） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 590565f15ac9d53b7209fa6808c4c24baeee6344
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182245"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>將結果集傳送到伺服器 (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳送結果集時[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，擴充預存程序應該呼叫適當的 API，如下所示：  
  
-   **Srv_sendmsg**之前或之後與已傳送所有資料列 （如果有的話），可能會以任何順序呼叫函式**srv_sendrow**。 所有訊息必須都傳送至用戶端，以都傳送完成狀態之前**srv_senddone**。  
  
-   系統會針對傳送到用戶端的每個資料列，呼叫 **srv_sendrow** 函式一次。 所有資料列必須傳送至用戶端之前任何訊息、 狀態值或完成狀態會傳送**srv_sendmsg**，則**srv_status**引數**srv_pfield**，或**srv_senddone**。  
  
-   尚未定義其資料行的資料列傳送**srv_describe**導致應用程式引發參考用錯誤訊息，並傳回給用戶端失敗。 在此情況下，不會傳送資料列。  
  
## <a name="see-also"></a>另請參閱  
 [建立擴充預存程序](creating-extended-stored-procedures.md)  
  
  
