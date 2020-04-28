---
title: SQLDriverConnect （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68171cfab2b65634433b107d829dd2a6e9b5c985
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307109"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLDriverConnect**可讓您連接到驅動程式，而不需要建立資料來源（DSN）。  
  
 下列關鍵字在所有驅動程式的連接字串中都受到支援： **DSN**、 **DBQ**和**FIL**。  
  
 也支援**PWD**關鍵字。 PWD 關鍵字不應包含任何特殊字元（請參閱**SQLGetInfo**傳回值中的 SQL_SPECIAL_CHARACTERS）。  
  
 當使用者開啟受密碼保護的檔案之後，不允許其他使用者開啟相同的檔案。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供搭配**SQLDriverConnect**使用之關鍵字/值組的範例。 如需 DRIVERID 值的完整清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。  
  
> [!NOTE]  
>  如果未指定 Paradox 驅動程式的 DBQ 或 DefaultDir，驅動程式將會連接到目前的目錄。  
  
|驅動程式|需要關鍵字|範例|  
|------------|-----------------------|-------------|  
|Paradox|驅動程式，DriverID|驅動程式 = {Microsoft Paradox 驅動程式（* .db）};DBQ = c：\temp; DriverID = 26|
