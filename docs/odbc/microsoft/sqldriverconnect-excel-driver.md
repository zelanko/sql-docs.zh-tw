---
title: "SQLDriverConnect （Excel 驅動程式） |Microsoft 文件"
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
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3db750232c45ce02b1dfe32e103d35ab20b366c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect （Excel 驅動程式）
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**可讓您連接至驅動程式，而不需要建立資料來源 (DSN)。  
  
 在連接字串的所有驅動程式支援下列關鍵字： **DSN**， **DBQ**，和**FIL**。  
  
 下表顯示最小的關鍵字，才能連接至每個驅動程式，並提供範例搭配使用的關鍵字/值組的**SQLDriverConnect**。 如需完整的 DRIVERID 值清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。  
  
> [!NOTE]  
>  如果未指定 DBQ 或 DefaultDir for Microsoft Excel 3.0 或 4.0 driver，驅動程式會連接到目前的目錄。  
  
|驅動程式|所需的關鍵字|範例|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 或 4.0|驅動程式 DriverID|Driver = {Microsoft Excel 驅動程式 (*.xls)};DBQ = c:\temp;DriverID = 278|  
|Microsoft Excel 5.0/7.0|驅動程式，DriverID DBQ|Driver = {Microsoft Excel 驅動程式 (*.xls)};DBQ=c:\temp\sample.xls;DriverID = 22|  
|Microsoft Excel 97 和更新版本|驅動程式，DriverID DBQ|Driver = {Microsoft Excel 驅動程式 (*.xls)};DBQ=c:\temp\sample.xls;DriverID = 790|
