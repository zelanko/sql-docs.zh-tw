---
title: 使用連接字串 :微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9083414503606720a40d372ed883a140953dc415
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307589"
---
# <a name="using-connection-strings"></a>使用連接字串
您可以使用連接字串連接到 Visual FoxPro 資料來源。  
  
 例如,要連接到 TasTrade 資料來源並覆寫與資料來源關聯的獨佔獨佔的目前設定,請使用字串:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 有關可以在連接字串包含的屬性關鍵字和值的清單,請參閱[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。  
  
 有關連接字串語法的完整說明,請參閱*ODBC 程式師參考*中的[SQLBrowseConnect。](../../odbc/reference/syntax/sqlbrowseconnect-function.md)
