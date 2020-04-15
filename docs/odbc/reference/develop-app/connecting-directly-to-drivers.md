---
title: 直接連接到驅動程式 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299078"
---
# <a name="connecting-directly-to-drivers"></a>直接連線到驅動程式
如本節前面在[選擇數據源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)時所討論的那樣,某些應用程式根本不希望使用數據源。 相反,他們希望直接連接到驅動程式。 **SQLDriverConnect**為應用程式提供了一種直接連接到驅動程式的方法,而無需指定數據源。 從概念上講,在運行時創建臨時數據源。  
  
 要直接連接到驅動程式,應用程式在連接字串中指定**DRIVER**關鍵字,而不是**DSN**關鍵字。 **DRIVER**關鍵字的值是**SQLDriver**傳回的驅動程式的說明。 例如,假設驅動程式具有描述悖論驅動程式,並且需要包含數據檔的目錄的名稱。 要連線到此驅動程式,應用程式可能使用以下連接字串之一:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 使用第一個字串時,驅動程式不需要任何其他資訊。 使用第二個字串時,驅動程式需要提示包含數據檔的目錄的名稱。
