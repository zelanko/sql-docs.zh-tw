---
title: "SQLDriverConnect (dBASE 驅動程式) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59ffc1188c1d98dc5697a65f69ab8792145f1ea3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**可讓您連接至驅動程式，而不需要建立資料來源 (DSN)。  
  
 在連接字串的所有驅動程式支援下列關鍵字： **DSN**， **DBQ**，和**FIL**。  
  
 使用 Paradox 驅動程式時，由使用者開啟受密碼保護的檔案之後，不允許其他使用者開啟相同的檔案。  
  
 下表顯示最小的關鍵字，才能連接至每個驅動程式，並提供範例搭配使用的關鍵字/值組的**SQLDriverConnect**。 如需完整的 DRIVERID 值清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。  
  
> [!NOTE]  
>  如果未指定 dBASEdriver 的 DBQ 或 DefaultDir，驅動程式會連接到目前的目錄。  
  
|驅動程式|所需的關鍵字|範例|  
|------------|-----------------------|--------------|  
|dBASE|驅動程式 DriverID|Driver = {Microsoft dBASE 驅動程式 (*.dbf)};DBQ = c:\temp;DriverID = 277|
