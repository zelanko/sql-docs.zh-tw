---
title: 附錄 g： 驅動程式的指導方針回溯相容性 |Microsoft 文件
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
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e84628c88937674ae5b2c1c992a40a8d3396cc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>附錄 g： 驅動程式的指導方針回溯相容性
本附錄提供驅動程式使用 ODBC 3 上的寫入器的資訊。*x*需要支援 ODBC 2 的驅動程式。*x*應用程式。 如需有關回溯相容性的詳細資訊，請參閱[回溯相容性和標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 此章節包含下列主題。  
  
-   [區塊資料指標，可捲動資料指標，ODBC 3.x 驅動程式的回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)— 新功能是在 ODBC 3 存在的功能。*x*而不是在 ODBC 2。*x*。 ODBC 3。*x*驅動程式通常不需要擔心回溯相容性的新功能，因為 ODBC 2。*x*應用程式永遠不會使用它們。 唯一的例外是與相關的功能**SQLFetch**， **SQLFetchScroll**， **SQLSetPos**，和**SQLExtendedFetch**; 如需詳細資訊資訊，請參閱稍後本附錄中。  
  
-   [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)— 重複功能是在 ODBC 3 以不同的方式實作的功能。*x*和 ODBC 2。*x*。 ODBC 3。*x*驅動程式不需要擔心重複的功能與回溯相容性，因為驅動程式管理員一律對應的 ODBC 2。*x* ODBC 3 的功能。*x*功能呼叫 ODBC 3 時。*x*驅動程式。 因此，ODBC 3。*x*驅動程式會看到只 ODBC 3。*x*功能。 如需有關這些對應，請參閱稍後本附錄中。  
  
-   [行為變更和 ODBC 3.x 驅動程式](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)： 行為變更的功能，在 ODBC 3 以不同方式處理。*x*和 ODBC 2。*x*。 ODBC 3。*x*驅動程式也不必擔心行為變更，並採取動作以回應由應用程式設定為 SQL_ATTR_ODBC_VERSION 環境屬性。
