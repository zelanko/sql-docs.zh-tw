---
title: 區塊資料指標、 可捲動的資料指標和回溯相容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3896473a1fa08f769f13d94bd1d81f373cf67c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854502"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>區塊資料指標、可捲動的資料指標和回溯相容性
兩者的存在**SQLFetchScroll**並**SQLExtendedFetch**表示 ODBC 之間應用程式發展介面 (API)，也就是函式集分割成先清除應用程式呼叫和服務提供者介面 (SPI)，也就是函式集驅動程式實作。 這種分割是必要的讓 ODBC 3。*x*，它會使用**SQLFetchScroll**，bealigned 的標準，而且也與 ODBC 2 相容。*x*，它會使用**SQLExtendedFetch**。  
  
 ODBC 3 *.x* API，這是一組函式應用程式會呼叫，包括**SQLFetchScroll**和相關的陳述式屬性。 ODBC 3 *.x* SPI，這是集合的函式，驅動程式會實作，包括**SQLFetchScroll**， **SQLExtendedFetch**，以及相關的陳述式屬性。 因為 ODBC 不會正式強制這種分割之間的 API 和 SPI，就可以針對 ODBC 3 *.x*應用程式呼叫**SQLExtendedFetch**和相關的陳述式屬性。 不過，沒有理由針對 ODBC 3 *.x*應用程式，若要這樣做。 如需 Api 和 Spi 的詳細資訊，請參閱 < 簡介[ODBC 架構](../../../odbc/reference/odbc-architecture.md)。  
  
 如需函式和陳述式屬性 ODBC 3。*x*應用程式應該使用與區塊和可捲動資料指標，請參閱[區塊資料指標、 可捲動的資料指標和 ODBC 3.x 應用程式的回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 此章節包含下列主題。  
  
-   [驅動程式管理員的作用](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驅動程式的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
