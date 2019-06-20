---
title: 連接到資料來源 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: adee8d8dd8d6db0d79b37ff853c41e7604fe21de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63302124"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>連線到資料來源 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 ODBC 應用程式可以數種方式傳遞的連接資訊。 比方說，應用程式可能會讓驅動程式一律會提示使用者輸入連接資訊。 或者，應用程式可能需要有指定的資料來源連接的連接字串。 連接到資料來源的方式取決於您的 ODBC 應用程式所使用的連線方式。  
  
 連接到資料來源的常見方式是透過 [資料來源] 對話方塊。 如果 ODBC 應用程式設定為使用對話方塊中，該對話方塊會隨即出現，並提示您輸入適當的資料來源連接資訊。  
  
 您也可以連接到資料來源，使用[連接字串](../../odbc/microsoft/connection-string-format-and-attributes.md)。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>若要連接到資料來源使用的對話方塊  
  
1.  [資料來源] 對話方塊出現時，選取與 Oracle 資料來源，然後按一下 [確定]。 [連接] 對話方塊隨即出現。  
  
2.  填寫 [連線] 對話方塊中，針對適當的資訊，然後按一下 [確定]。  
  
 連接後會驗證資訊，您的應用程式可以使用 ODBC Driver for Oracle 來存取資料來源包含的資訊。
