---
title: ODBC 元件 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb58971a193a210f927d1b0a38f2be671b749468
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="affected-odbc-components"></a>受影響的 ODBC 元件
回溯相容性會描述如何影響所引進的新版本的驅動程式管理員中的應用程式、 驅動程式管理員，以及驅動程式。 這會影響應用程式和驅動程式時一個或兩個它們留在舊版本。 有，因此，三種類型的回溯相容性，需要考慮下表所示。  
  
|型別|資料採礦的版本|應用程式版本|驅動程式版本|  
|----------|-------------------|----------------------------|-----------------------|  
|為了與舊版相容的驅動程式管理員|3*.x*|2。*x*|2。*x*|  
|[1] 的驅動程式的回溯相容性|3*.x*|2。*x*|3。*x*|  
|應用程式的回溯相容性|3。*x*|3。*x*|2。*x*|  
  
 [1] 的驅動程式的回溯相容性主要述附錄 g： 驅動程式的指導方針的回溯相容性。  
  
> [!NOTE]  
>  符合標準的應用程式 — 例如，已寫入根據 Open Group 或 ISO CLI 標準的應用程式 — 保證可以運作 ODBC 3*.x*驅動程式透過 ODBC 3*.x*驅動程式管理員。 它會假設應用程式使用的功能是可用的驅動程式中。 同時也假設符合標準的應用程式，已編譯 ODBC 3*.x*標頭檔。
