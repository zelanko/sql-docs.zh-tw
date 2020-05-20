---
title: 中斷連接並重新連接記錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ef30165a05bc472bfe34cec4e7f669d545d7768
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761054"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>中斷並重新連線資料錄集
ADO 中最強大的功能之一，就是從資料來源開啟用戶端記錄集，然後將記錄集與資料來源中斷連接的功能。 當記錄集中斷連接之後，就可以關閉與資料來源的連接，藉此釋放用來維護它的伺服器上的資源。 當記錄集已中斷連線，並于稍後重新連接至資料來源，並以批次模式傳送更新時，您可以繼續查看和編輯其中的資料。  
  
 若要中斷記錄集的連接，請以 adUseClient 的資料指標位置開啟它，然後將 ActiveConnection 屬性設定為等於 [無]。 （C + + 使用者應該將 ActiveConnection 設定為等於 Null 以中斷連線）。  
  
 當我們討論記錄集持續性時，我們將會使用離線式記錄集，以解決需要在用戶端電腦未連線到網路時，可供應用程式使用的記錄集中資料的案例。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
