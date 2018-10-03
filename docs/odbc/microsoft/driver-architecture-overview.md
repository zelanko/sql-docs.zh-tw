---
title: 驅動程式架構概觀 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0fdb1789c6640c072ec013c341bd4889b28bb469
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771866"
---
# <a name="driver-architecture-overview"></a>驅動程式架構概觀
Microsoft Visual FoxPro ODBC Driver 是 32 位元驅動程式，可讓您開啟並查詢 Microsoft Visual FoxPro 資料庫或透過開啟資料庫連接 (ODBC) 介面的 FoxPro 資料表。 您可以使用下列類型的應用程式的 FoxPro 資料：  
  
-   Microsoft Office 應用程式，例如 Microsoft Excel 或 Microsoft Word，會使用 Microsoft 查詢來使用 ODBC 通訊。  
  
-   Microsoft Visual c + + 中使用 ODBC SDK API 的 C 撰寫的應用程式。  
  
-   Microsoft Visual Basic 或 Microsoft Visual Basic for Applications 中撰寫的應用程式。  
  
 在每個案例中，要求的資訊，請使用 ODBC API。 ODBC 驅動程式管理員會搭配 Visual FoxPro ODBC Driver，以開啟，並從 FoxPro 資料表和資料庫擷取資料。  
  
 在下圖中表示的架構：  
  
 ![顯示 ODBC 驅動程式架構](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 此章節包含下列主題。  
  
-   [Visual FoxPro 術語](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [安裝和設定 Visual FoxPro ODBC Driver](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [使用 Visual FoxPro ODBC Driver](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
