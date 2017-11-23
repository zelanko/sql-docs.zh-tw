---
title: "依序數載入 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d23eccad532e57b754e1305e1381613938cd6168
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="loading-by-ordinal"></a>依序數載入
在 ODBC 2。*x*，無法執行載入依序數，以改善連線程序的效能。 ODBC 2。*x*驅動程式匯出序數 199 虛擬函式，則當驅動程式管理員偵測到它，根據序數而不是依名稱解析的 ODBC 函式的位址。 這項功能仍支援 ODBC 2。*x*驅動程式，但是不支援 ODBC 3*.x*驅動程式。
