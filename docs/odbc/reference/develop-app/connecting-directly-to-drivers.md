---
title: 直接連接到驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6aacb5d3df985949e04cdd47a9fe460cddbde6a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299078"
---
# <a name="connecting-directly-to-drivers"></a>直接連線到驅動程式
如同在本節稍早的[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)中所討論，有些應用程式根本不想使用資料來源。 相反地，他們想要直接連接到驅動程式。 **SQLDriverConnect**提供了一種方法，讓應用程式直接連接到驅動程式，而不需要指定資料來源。 在概念上，會在執行時間建立暫存資料來源。  
  
 若要直接連接到驅動程式，應用程式會在連接字串中指定**driver**關鍵字，而不是使用**DSN**關鍵字。 **Driver**關鍵字的值是**SQLDrivers**所傳回之驅動程式的描述。 例如，假設驅動程式的 description 是 Paradox 驅動程式，而且需要包含資料檔案的目錄名稱。 若要連接到此驅動程式，應用程式可能會使用下列其中一個連接字串：  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 使用第一個字串，驅動程式不需要任何額外的資訊。 使用第二個字串時，驅動程式必須提示輸入包含資料檔案的目錄名稱。
