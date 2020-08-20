---
description: 建立及終止執行緒
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
ms.openlocfilehash: c0100b85bc596149d809dee7e6c4cb3547dbd081
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465850"
---
# <a name="creating-and-terminating-threads"></a>建立及終止執行緒
使用 ODBC 的多執行緒應用程式應該呼叫 Microsoft® Visual C++®執行時間程式庫函數 **_beginthread** 和 **_endthread** (或 **_beginthreadex** 和 **_endthreadex**) ，以建立和結束通話 ODBC 驅動程式管理員的執行緒。 如果應用程式呼叫 Microsoft Windows NT®函式 **CreateThread** 和 **EndThread** ，則會發生記憶體流失，因為驅動程式管理員和某些 ODBC 驅動程式會呼叫 C 執行時間函式，這些函式在呼叫 **CreateThread**所建立的執行緒上無法運作。 如需詳細資訊，請參閱 Microsoft Windows®檔。
