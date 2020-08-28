---
description: 中斷並重新連線資料錄集
title: 中斷和重新連接記錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f8a759ed099f51e1256a8e4701c0aed34a3ff03
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991369"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>中斷並重新連線資料錄集
ADO 中最強大的功能之一，就是從資料來源開啟用戶端記錄集，然後中斷記錄集與資料來源的連接。 當記錄集中斷連接之後，就可以關閉資料來源的連接，藉此釋放用來維護它的伺服器資源。 您可以在記錄集中斷連接時，繼續查看和編輯記錄集內的資料，稍後再重新連接到資料來源，並以批次模式傳送您的更新。  
  
 若要中斷記錄集的連接，請使用 adUseClient 的資料指標位置開啟它，然後將 ActiveConnection 屬性設定為等於 Nothing。  (c + + 使用者應該將 ActiveConnection 設為等於 Null，以中斷連線。 )   
  
 當我們討論記錄集持續性以解決需要在用戶端電腦未連線到網路的情況下，將記錄集中的資料提供給應用程式的案例時，我們將會使用此區段中的中斷連接記錄集。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](./batch-mode.md)