---
title: "使用連接字串 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc75f4b4b90f2845ea18d6e3208806fce2c9179e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="using-connection-strings"></a>使用連接字串
您可以使用的連接字串連接至 Visual FoxPro 資料來源。  
  
 例如，若要連接的 TasTrade 資料來源和覆寫目前專有的設定相關聯的資料來源，您會使用字串：  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 如需屬性的關鍵字，您可以在連接字串中包含的值，請參閱[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。  
  
 如需連接字串語法的完整說明，請參閱[SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md)中*ODBC 程式設計人員參考*。
