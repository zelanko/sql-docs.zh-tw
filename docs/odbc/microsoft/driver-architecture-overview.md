---
title: 驅動程式架構總覽 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 833c953df3502eb7e5d5676da8df057734174619
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071925"
---
# <a name="driver-architecture-overview"></a>驅動程式架構概觀
Microsoft Visual FoxPro ODBC Driver 是一個32位驅動程式，可讓您透過開放式資料庫連接（ODBC）介面，開啟及查詢 Microsoft Visual FoxPro 資料庫或 FoxPro 資料表。 您可以使用下列類型的應用程式來存取 FoxPro 資料：  
  
-   Microsoft Office 的應用程式（例如 Microsoft Excel 或 Microsoft Word），會使用 Microsoft Query 與 ODBC 進行通訊。  
  
-   以 Microsoft Visual C++ 或 C 撰寫並使用 ODBC SDK API 的應用程式。  
  
-   以 Microsoft Visual Basic 或 Microsoft Visual Basic for Applications 撰寫的應用程式。  
  
 在每個案例中，資訊的要求都會使用 ODBC API。 ODBC 驅動程式管理員可與 Visual FoxPro ODBC 驅動程式搭配使用，以開啟和抓取 FoxPro 資料表和資料庫中的資料。  
  
 架構會在下圖中表示：  
  
 ![顯示 ODBC 驅動程式架構](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 此章節包含下列主題。  
  
-   [Visual FoxPro 術語](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安裝和設定 Visual FoxPro ODBC 驅動程式](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC Driver](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
