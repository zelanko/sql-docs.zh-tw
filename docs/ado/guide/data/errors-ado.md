---
description: 錯誤 (ADO)
title: ADO)  (錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 8ae6611b-3069-4155-b014-c0c9da37be39
author: rothja
ms.author: jroth
ms.openlocfilehash: 392d1f2fdfc0a7fe2e0cf9e1e14efb77f396acfd
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806128"
---
# <a name="errors-ado"></a>錯誤 (ADO)
涉及 ADO 物件的任何作業都可以產生一或多個提供者錯誤。 當發生每個錯誤時，會將一個或多個**錯誤**物件放在**連接**物件的**Errors**集合中。 如需有關在 ADO 應用程式中處理警告和錯誤的詳細資訊，請參閱 [錯誤處理](./error-handling.md)。  
  
 應用程式錯誤可由不同的機制引發。 例如，在 Visual Basic 中， **Err** 物件將會包含應用層級的錯誤。