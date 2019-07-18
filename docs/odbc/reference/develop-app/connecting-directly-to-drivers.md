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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44b9de304069849e965fc335e130ae57d9ec8bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083159"
---
# <a name="connecting-directly-to-drivers"></a>直接連線到驅動程式
如所述[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)稍早在此區段中，某些應用程式不會希望完全使用資料來源。 相反地，他們想要直接連接到驅動程式。 **SQLDriverConnect**可讓應用程式直接連接到驅動程式但未指定資料來源。 就概念而言，就會在執行階段建立暫存的資料來源。  
  
 若要直接連接驅動程式，應用程式指定**驅動程式**而不是在連接字串中的關鍵字**DSN**關鍵字。 值**驅動程式**關鍵字是驅動程式的描述，所傳回的**SQLDrivers**。 例如，假設有描述 Paradox 驅動程式的驅動程式，以及需要包含資料檔案的目錄名稱。 若要連接到這個驅動程式，應用程式可能會使用其中一個下列的連接字串：  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 第一個字串，此驅動程式就不需要任何額外的資訊。 第二個字串，此驅動程式需要提示您輸入包含資料檔案的目錄名稱。
