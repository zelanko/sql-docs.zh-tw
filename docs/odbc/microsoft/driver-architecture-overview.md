---
title: 驅動程式架構概觀 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f9c5d4720e126c6d496754201889b862b508e90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="driver-architecture-overview"></a>驅動程式架構概觀
Microsoft Visual FoxPro ODBC 驅動程式是 32 位元驅動程式，可讓您開啟和查詢 Microsoft Visual FoxPro 資料庫或透過開啟資料庫連接 (ODBC) 介面 FoxPro 資料表。 您可以存取 FoxPro 資料使用下列類型的應用程式：  
  
-   Microsoft Office 應用程式，例如 Microsoft Excel 或 Microsoft Word，會使用 Microsoft 查詢與 ODBC 進行通訊。  
  
-   Microsoft Visual c + + 中使用 ODBC SDK API 的 C 撰寫的應用程式。  
  
-   Microsoft Visual Basic 或 Microsoft Visual Basic for Applications 中撰寫的應用程式。  
  
 在每個案例中，要求的資訊，請使用 ODBC API。 ODBC 驅動程式管理員搭配 Visual FoxPro ODBC 驅動程式，以開啟，並從 FoxPro 資料表和資料庫擷取資料。  
  
 下圖是以表示架構：  
  
 ![顯示 ODBC 驅動程式架構](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 此章節包含下列主題。  
  
-   [Visual FoxPro 術語](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安裝和設定 Visual FoxPro ODBC 驅動程式](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC Driver](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
