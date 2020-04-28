---
title: 從資料來源或驅動程式中斷連線 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300458"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>從資料來源或驅動程式中斷連線
當應用程式完成使用資料來源時，它會呼叫**SQLDisconnect**。 **SQLDisconnect**會釋放在連接上配置的任何語句，並中斷驅動程式與資料來源的連線。 如果交易正在處理中，它會傳回錯誤。  
  
 中斷連線之後，應用程式可以呼叫**SQLFreeHandle**來釋放連接。 在釋放連接之後，應用程式設計錯誤是在 ODBC 函式的呼叫中使用連接的控制碼。這麼做並沒有定義，但可能會產生嚴重的後果。 呼叫**SQLFreeHandle**時，驅動程式會釋放用來儲存連接相關資訊的結構。  
  
 應用程式也可以重複使用連接，以連接到不同的資料來源，或重新連接到相同的資料來源。 決定維持線上狀態，而不是在稍後中斷連接和重新連接，需要應用程式寫入器考慮每個選項的相對成本;連接到資料來源和剩餘連接的工作，可能會相對於連接媒體而耗費較高的成本。 在進行正確的取捨時，應用程式也必須針對相同資料來源上的進一步作業做出可能性和時間的假設。
