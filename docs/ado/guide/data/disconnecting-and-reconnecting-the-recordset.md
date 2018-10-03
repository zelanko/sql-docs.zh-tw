---
title: 中斷並重新連接資料錄集 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0cefdb81aa9e9a1a5f7ad7ba1f6db86d1ae95e2d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771996"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>中斷並重新連線資料錄集
在 ADO 中找到的最強大功能之一是從資料來源開啟用戶端的資料錄集，然後再中斷資料來源中的資料錄集的功能。 一旦已中斷連接資料錄集，資料來源的連接可以關閉，藉此釋放用來對它進行維護的伺服器上的資源。 您可以繼續檢視和編輯資料錄集中的資料，而它已中斷連線和稍後重新連線到資料來源，並傳送您的更新，批次模式。  
  
 若要中斷連線的資料錄集，請開啟且 adUseClient，資料指標位置，然後將 ActiveConnection 屬性等於 Nothing。 （c + + 使用者應該設定 ActiveConnection 等於 NULL 中斷連線）。  
  
 我們稍後會使用已中斷連線的資料錄集這一節討論資料錄集的持續性，以解決的問題，我們要在用戶端電腦未連線到網路時，應用程式可使用資料錄集中有資料時。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
