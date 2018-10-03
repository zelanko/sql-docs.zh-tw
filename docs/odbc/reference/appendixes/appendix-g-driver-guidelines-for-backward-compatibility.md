---
title: 附錄 g： 回溯相容性的驅動程式指導方針 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63f999fa01623898be6561c9f5a450c6ec81487d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654226"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>附錄 G：回溯相容性的驅動程式方針
本附錄提供使用 ODBC 3 上的驅動程式寫入器的資訊。*x*驅動程式，需要支援 ODBC 2。*x*應用程式。 如需有關回溯相容性的詳細資訊，請參閱 <<c0> [ 回溯相容性與標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 此章節包含下列主題。  
  
-   [區塊資料指標、 可捲動的資料指標和 ODBC 3.x 驅動程式的回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)-新功能是在 ODBC 3 存在的功能。*x*而不是在 ODBC 2。*x*。 ODBC 3。*x*驅動程式通常不需要擔心回溯相容性的新功能，因為 ODBC 2。*x*應用程式永遠不會使用它們。 唯一例外是與相關的功能**SQLFetch**， **SQLFetchScroll**， **SQLSetPos**，以及**SQLExtendedFetch**; 如需詳細資訊資訊，請參閱稍後本附錄中。  
  
-   [對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)— 重複功能是在 ODBC 3 的實作方式不同。*x*和 ODBC 2。*x*。 ODBC 3。*x*驅動程式就不必擔心重複的功能與回溯相容性，因為驅動程式管理員始終對應的 ODBC 2。*x* ODBC 3 的功能。*x*功能時呼叫 ODBC 3。*x*驅動程式。 因此，ODBC 3。*x*驅動程式會看到只 ODBC 3。*x*功能。 如需這些對應，請參閱稍後本附錄中。  
  
-   [行為變更和 ODBC 3.x 驅動程式](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)— 行為變更會在 ODBC 3 以不同方式處理的功能。*x*和 ODBC 2。*x*。 ODBC 3。*x*驅動程式也不必擔心的行為變更，並採取動作以回應應用程式設定為 SQL_ATTR_ODBC_VERSION 環境屬性。
