---
title: 區塊資料指標、可滾動游標和回溯相容性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe24362f1a49577a7fb494f768947080d0ab6e9e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292308"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>區塊資料指標、可捲動的資料指標和回溯相容性
**SQLFetchScroll**和**SQLExtendedFetch**兩者都代表應用程式開發介面（API）之間的第一次明確分割，也就是應用程式所呼叫的函式集，以及服務提供者介面（SPI），這是驅動程式所執行的一組函數。 這是必要的分割，如此一來，使用**SQLFetchScroll**、bealigned 與標準，而且也與使用**SQLExtendedFetch***的 odbc 2.x*相容*的 odbc 3.x。*  
  
 *ODBC 3.X* API，這是應用程式所呼叫的一組函式，包括**SQLFetchScroll**和相關的語句屬性。 *ODBC 3.X* SPI，這是驅動程式所實作用的一組函式，包括**SQLFetchScroll**、 **SQLExtendedFetch**和相關的語句屬性。 因為 ODBC 不會在 API 與 SPI 之間正式地強制執行這種分割，所以 ODBC 3.x*應用程式*可能會呼叫**SQLExtendedFetch**和相關的語句屬性。 不過 *，ODBC 3.x*應用程式沒有理由這麼做。 如需 Api 和 SPIs 的詳細資訊，請參閱[ODBC 架構](../../../odbc/reference/odbc-architecture.md)簡介。  
  
 如需 ODBC *3.x 應用程式*應該搭配區塊和可滾動資料指標使用之函數和語句屬性的相關資訊，請參閱[Odbc 3.x 應用程式的區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 此章節包含下列主題。  
  
-   [驅動程式管理員的作用](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驅動程式的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
