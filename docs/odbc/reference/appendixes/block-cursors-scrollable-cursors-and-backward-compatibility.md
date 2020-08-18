---
description: 區塊資料指標、可捲動的資料指標和回溯相容性
title: 區塊資料指標、可滾動的資料指標和回溯相容性 |Microsoft Docs
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
ms.openlocfilehash: 46f6d3611b0a55325387f2c7723734500d48af83
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411294"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>區塊資料指標、可捲動的資料指標和回溯相容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在都代表 ODBC 在應用程式開發介面 (API) （應用程式所呼叫的函式集合）之間的第一個明確分割，而服務提供者介面 (SPI) ，也就是驅動程式所執行的一組函數。 這是必要的分割，如此一來，使用**SQLFetchScroll**、bealigned 與標準且也*與 odbc 2.X*相容*的 odbc 3.x*會使用**SQLExtendedFetch**。  
  
 *ODBC 3.X* API 是應用程式呼叫的函式集合，其中包含**SQLFetchScroll**和相關的語句屬性。 *ODBC 3.X* SPI 是驅動程式所執行的一組函數，包括**SQLFetchScroll**、 **SQLExtendedFetch**和相關的語句屬性。 由於 ODBC 不會在 API 與 SPI 之間正式強制執行這項分割， *因此 ODBC 3.x* 應用程式可能會呼叫 **SQLExtendedFetch** 和相關的語句屬性。 不過 *，ODBC 3.x* 應用程式沒有理由這麼做。 如需 Api 和 SPIs 的詳細資訊，請參閱 [ODBC 架構](../../../odbc/reference/odbc-architecture.md)簡介。  
  
 如需 ODBC 3.x *應用程式應* 使用的函式和語句屬性的相關資訊，請參閱 [Odbc 3.x 應用程式的區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 此章節包含下列主題。  
  
-   [驅動程式管理員的作用](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驅動程式的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
