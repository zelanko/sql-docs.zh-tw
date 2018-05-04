---
title: 依序數載入 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db3a9e517d70f19ad72e2991ca021013939a7db4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="loading-by-ordinal"></a>依序數載入
在 ODBC 2。*x*，無法執行載入依序數，以改善連線程序的效能。 ODBC 2。*x*驅動程式匯出序數 199 虛擬函式，則當驅動程式管理員偵測到它，根據序數而不是依名稱解析的 ODBC 函式的位址。 這項功能仍支援 ODBC 2。*x*驅動程式，但是不支援 ODBC 3 *.x*驅動程式。
