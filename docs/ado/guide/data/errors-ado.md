---
title: 錯誤（ADO） |Microsoft Docs
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
ms.openlocfilehash: b014e68bce1e0fbcbabb9c8ee314ee7a9d6e7311
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761004"
---
# <a name="errors-ado"></a>錯誤 (ADO)
任何牽涉到 ADO 物件的作業都可能產生一個或多個提供者錯誤。 當發生每個錯誤時，會將一個或多個**錯誤**物件放在**Connection**物件的**Errors**集合中。 如需在 ADO 應用程式中處理警告和錯誤的詳細資訊，請參閱[錯誤處理](../../../ado/guide/data/error-handling.md)。  
  
 應用程式錯誤可以透過不同的機制來引發。 例如，在 Visual Basic 中， **Err**物件將會包含應用層級錯誤。
