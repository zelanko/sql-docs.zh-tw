---
title: 使用連接字串 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77bc54f857e04f31ccb982ca40b3ed6334664870
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633203"
---
# <a name="using-connection-strings"></a>使用連接字串
您可以使用的連接字串來連接到 Visual FoxPro 資料來源。  
  
 比方說，若要連接到 TasTrade 資料來源並覆寫目前的互斥設定相關聯的資料來源，您會使用字串：  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 如需屬性的關鍵字，您可以在連接字串中包含的值，請參閱[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。  
  
 如需連接字串語法的完整說明，請參閱 < [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md)中*ODBC 程式設計人員參考*。
