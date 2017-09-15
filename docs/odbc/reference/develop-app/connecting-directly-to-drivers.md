---
title: "直接連接到驅動程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bacb659cb6986f86151502998523ade468f7cedd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-directly-to-drivers"></a>直接連接到驅動程式
中所述的[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)稍早在本章節，某些應用程式不會希望完全使用資料來源。 相反地，他們想要直接連接到驅動程式。 **SQLDriverConnect**提供方法，讓應用程式直接連接到驅動程式但未指定資料來源。 在概念上，於執行階段建立暫存資料來源。  
  
 若要直接連接到驅動程式，應用程式指定**驅動程式**而不是在連接字串中的關鍵字**DSN**關鍵字。 值**驅動程式**關鍵字是驅動程式的描述，所傳回**SQLDrivers**。 例如，假設驅動程式具有描述 Paradox 驅動程式，以及需要包含資料檔案的目錄名稱。 若要連接到這個驅動程式，應用程式可能會使用下列連接字串：  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 第一個字串，此驅動程式不需要任何額外的資訊。 第二個字串，此驅動程式需要提示您輸入包含資料檔案的目錄名稱。
