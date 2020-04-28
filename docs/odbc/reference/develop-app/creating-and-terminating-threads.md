---
title: 建立和終止執行緒 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3536deef604d7dbf645903e7d171a58cd9fec96a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301689"
---
# <a name="creating-and-terminating-threads"></a>建立及終止執行緒
使用 ODBC 的多執行緒應用程式應該呼叫 Microsoft® Visual C++®執行時間程式庫函式 **_beginthread**和 **_endthread** （或 **_beginthreadex**和 **_ENDTHREADEX**）來建立及結束通話 ODBC 驅動程式管理員的執行緒。 如果應用程式呼叫 Microsoft Windows NT®函式**CreateThread**和**EndThread** ，就會發生記憶體流失，因為驅動程式管理員和某些 ODBC 驅動程式會呼叫 C 執行時間函式，而這些函數無法在呼叫**CreateThread**所建立的執行緒上運作。 如需詳細資訊，請參閱 Microsoft Windows®檔。
