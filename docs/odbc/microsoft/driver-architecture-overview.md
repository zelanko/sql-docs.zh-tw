---
title: 驅動程式體系結構概述 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd55290e09fbd35f5a1559ce4209693ef8eaaf73
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303459"
---
# <a name="driver-architecture-overview"></a>驅動程式架構概觀
Microsoft Visual FoxPro ODBC 驅動程式是一個 32 位元驅動程式,使您能夠透過開放資料庫連接 (ODBC) 介面打開和查詢 Microsoft Visual FoxPro 資料庫或 FoxPro 表。 您可以使用以下類型的應用程式存取 FoxPro 資料:  
  
-   使用微軟查詢與 ODBC 通訊的微軟 Office 應用程式,如 Microsoft Excel 或 Microsoft Word。  
  
-   使用 ODBC SDK API 在 Microsoft 視覺C++或 C 編寫的應用程式。  
  
-   以 Microsoft 視覺化基本版或 Microsoft 應用程式視覺基本版編寫的應用程式。  
  
 在每種情況下,資訊請求都使用 ODBC API。 ODBC 驅動程式管理員與 Visual FoxPro ODBC 驅動程式合作,從 FoxPro 表和資料庫打開和檢索數據。  
  
 體系結構在下圖中表示:  
  
 ![顯示 ODBC 驅動程式架構結構](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 此章節包含下列主題。  
  
-   [Visual FoxPro 術語](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安裝並設定視覺化福斯Pro ODBC驅動程式](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC Driver](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
