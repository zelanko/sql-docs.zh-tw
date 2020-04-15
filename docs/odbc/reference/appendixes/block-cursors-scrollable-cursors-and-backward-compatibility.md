---
title: 塊游標、可滾動游標和向后相容性 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292308"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>區塊資料指標、可捲動的資料指標和回溯相容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在代表了在 ODBC 中,應用程式程式設計介面 (API) 和服務提供者介面 (SPI) 之間的第一個明確拆分,這是驅動程式實現的函數集。 這種分割是必要的,以便使用**SQLFetchScroll**的 ODBC *3.x*與標準保持一致,並且與使用**SQLAt2.x**的 ODBC *2.x*相容 。  
  
 ODBC *3.x* API 是應用程式呼叫的功能集,包括**SQLFetchScroll**和相關語句屬性。 ODBC *3.x* SPI 是驅動程式實現的函數集,包括**SQLFetchScroll、SQL****擴展獲取**和相關語句屬性。 由於 ODBC 未正式強制 API 和 SPI 之間的此拆分,因此 ODBC *3.x*應用程式可以呼叫**SQLExtendedFetch**和相關語句屬性。 但是,ODBC *3.x*應用程式沒有理由這樣做。 有關 API 和 API 的詳細資訊,請參閱[ODBC 體系結構](../../../odbc/reference/odbc-architecture.md)的簡介。  
  
 有關 ODBC *3.x*應用程式應使用哪些函數和敘述屬性的資訊,請參閱[區塊游標、可滾動游標和 ODBC 3.x 應用程式的向後相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 此章節包含下列主題。  
  
-   [驅動程式管理員的作用](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驅動程式的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
