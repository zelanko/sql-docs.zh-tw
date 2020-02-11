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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002079"
---
# <a name="creating-and-terminating-threads"></a>建立及終止執行緒
使用 ODBC 的多執行緒應用程式應該呼叫 Microsoft® Visual C++®執行時間程式庫函式 **_beginthread**和 **_endthread** （或 **_beginthreadex**和 **_ENDTHREADEX**）來建立及結束通話 ODBC 驅動程式管理員的執行緒。 如果應用程式呼叫 Microsoft Windows NT®函式**CreateThread**和**EndThread** ，就會發生記憶體流失，因為驅動程式管理員和某些 ODBC 驅動程式會呼叫 C 執行時間函式，而這些函數無法在呼叫**CreateThread**所建立的執行緒上運作。 如需詳細資訊，請參閱 Microsoft Windows®檔。
