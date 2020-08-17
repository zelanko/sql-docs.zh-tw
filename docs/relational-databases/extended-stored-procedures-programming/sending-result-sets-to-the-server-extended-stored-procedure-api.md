---
description: 將結果集傳送到伺服器 (擴充預存程序 API)
title: 將結果集傳送到伺服器 (擴充預存程序 API)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 4747c464956d4c1da804a4bf9182cbb507a45989
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88383134"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>將結果集傳送到伺服器 (擴充預存程序 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 將結果集傳送至時 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，擴充預存程式應該呼叫適當的 API，如下所示：  
  
-   **Srv_sendmsg**函數可以在所有資料列之前或之後的任何順序中呼叫， (是否已傳送**srv_sendrow**的任何) 。 所有訊息都必須先傳送至用戶端，才能使用 **srv_senddone**傳送完成狀態。  
  
-   系統會針對傳送到用戶端的每個資料列，呼叫 **srv_sendrow** 函式一次。 所有資料列都必須先傳送至用戶端，才能使用**srv_sendmsg**、 **srv_pfield**的**srv_status**引數或**srv_senddone**傳送任何訊息、狀態值或完成狀態。  
  
-   傳送尚未以 **srv_describe** 定義之所有資料行的資料列，會導致應用程式引發參考用錯誤訊息，並將失敗傳回用戶端。 在此情況下，不會傳送資料列。  
  
## <a name="see-also"></a>另請參閱  
 [建立擴充預存程序](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
