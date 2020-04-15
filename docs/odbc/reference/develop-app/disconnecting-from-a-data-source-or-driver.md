---
title: 斷開與資料源或驅動程式的連線 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 154a571bce3a337d539216ce89c32420ab981bd8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300458"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>從資料來源或驅動程式中斷連線
當應用程式完成使用資料來源後,它將呼叫**SQLDisconnect**。 **SQLDisconnect**釋放在連接上分配的任何語句,並將驅動程序與數據源斷開連接。 如果事務正在處理中,它將返回錯誤。  
  
 斷開連接後,應用程式可以調用**SQLFreeHandle**來釋放連接。 釋放連接後,在調用 ODBC 函數時使用連接的句柄是應用程式程式設計錯誤;這樣做有未定義,但可能是致命的後果。 調用**SQLFreeHandle**時,驅動程式將釋放用於存儲有關連接的資訊的結構。  
  
 應用程式還可以重用連接,以連接到其他數據源或重新連接到同一數據源。 保持連接的決定,而不是以後斷開連接和重新連接,要求應用程式編寫器考慮每個選項的相對成本;連接到數據源和保持連接可能相對昂貴,具體取決於連接介質。 在進行正確的權衡時,應用程式還必須對在同一數據源上進行進一步操作的可能性和時間進行假設。
