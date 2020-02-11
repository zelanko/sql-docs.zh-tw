---
title: SQLDriverConnect （Excel 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e38f2f513b7da2c9342470ba75e2ee11b3d7e52a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053899"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLDriverConnect**可讓您連接到驅動程式，而不需要建立資料來源（DSN）。  
  
 下列關鍵字在所有驅動程式的連接字串中都受到支援： **DSN**、 **DBQ**和**FIL**。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供搭配**SQLDriverConnect**使用之關鍵字/值組的範例。 如需 DRIVERID 值的完整清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。  
  
> [!NOTE]  
>  如果未針對 Microsoft Excel 3.0 或4.0 驅動程式指定 DBQ 或 DefaultDir，驅動程式將會連接到目前的目錄。  
  
|驅動程式|需要關鍵字|範例|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 或4。0|驅動程式，DriverID|驅動程式 = {Microsoft Excel 驅動程式（* .xls）};DBQ = c：\temp;DriverID = 278|  
|Microsoft Excel 5.0/7。0|Driver、DriverID、DBQ|驅動程式 = {Microsoft Excel 驅動程式（* .xls）};DBQ = c:\temp\sample.xls;DriverID = 22|  
|Microsoft Excel 97 和更新版本|Driver、DriverID、DBQ|驅動程式 = {Microsoft Excel 驅動程式（* .xls）};DBQ = c:\temp\sample.xls;DriverID = 790|
