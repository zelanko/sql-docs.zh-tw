---
title: 建立和終止線程 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301689"
---
# <a name="creating-and-terminating-threads"></a>建立及終止執行緒
使用 ODBC 的多線程應用程式應呼叫 Microsoft® 視覺化 C++®執行時庫函數 **_beginthread,_endthread(** 或 **_beginthreadex**和 **_endthreadex),** 以建立和終止呼叫 **_endthread**ODBC 驅動程式管理器的線程。 如果應用程式呼叫 Microsoft Windows NT®函數**CreateThread**和**EndThread,** 則記憶體洩漏將發生,因為驅動程式管理器和某些 ODBC 驅動程式呼叫 C 執行時函數,這些函數不適用於透過調用**CreateThread**創建的線程。 有關詳細資訊,請參閱 Microsoft Windows®文檔。
