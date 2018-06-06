---
title: SQLDriverConnect （Paradox 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5437dca7911b2931378a51b8ba16538286858b65
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect （Paradox 驅動程式）
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**可讓您連接至驅動程式，而不需要建立資料來源 (DSN)。  
  
 在連接字串的所有驅動程式支援下列關鍵字： **DSN**， **DBQ**，和**FIL**。  
  
 **PWD**也支援關鍵字。 PWD 關鍵字不應包含任何特殊字元 (請參閱在 SQL_SPECIAL_CHARACTERS **SQLGetInfo**傳回值)。  
  
 使用者已開啟密碼保護的檔案之後，不允許其他使用者開啟相同的檔案。  
  
 下表顯示最小的關鍵字，才能連接至每個驅動程式，並提供範例搭配使用的關鍵字/值組的**SQLDriverConnect**。 如需完整的 DRIVERID 值清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。  
  
> [!NOTE]  
>  如果未指定 DBQ 或 DefaultDir Paradox 驅動程式，驅動程式會連接到目前的目錄。  
  
|驅動程式|所需的關鍵字|範例|  
|------------|-----------------------|-------------|  
|Paradox|驅動程式 DriverID|Driver={Microsoft Paradox Driver (*.db )}; DBQ=c:\temp;DriverID=26|
