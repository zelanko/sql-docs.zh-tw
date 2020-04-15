---
title: SQLDriver連接(Excel驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1108206bf38183887540b114fda5a1e913aa67d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307119"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Excel 驅動程式)
> [!NOTE]  
>  本主題提供特定於 Excel 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLDriverConnect**使您能夠連接到驅動程式,而無需創建資料源 (DSN)。  
  
 所有驅動程式的連接字串都支援以下關鍵字 **:DSN、DBQ****DBQ**和**FIL**。  
  
 下表顯示了連接到每個驅動程式所需的最小關鍵字,並提供了**SQLDriverConnect**一起使用的關鍵字/值對的範例。 有關 DRIVERID 值的完整清單,請參考[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。  
  
> [!NOTE]  
>  如果未為 Microsoft Excel 3.0 或 4.0 驅動程式指定 DBQ 或 DefaultDir,則驅動程式將連接到當前目錄。  
  
|驅動程式|需要關鍵字|範例|  
|------------|-----------------------|--------------|  
|微軟 Excel 3.0 或 4.0|驅動程式,驅動程式識別碼|驅動程式[微軟 Excel 驅動程式 (*.xls)];DBQ_c:\temp;驅動程式識別碼=278|  
|微軟 Excel 5.0/7.0|驅動程式、驅動程式 ID、DBQ|驅動程式[微軟 Excel 驅動程式 (*.xls)];DBQ_c:\temp_sample.xls;驅動程式識別碼=22|  
|微軟 Excel 97 及更高版本|驅動程式、驅動程式 ID、DBQ|驅動程式[微軟 Excel 驅動程式 (*.xls)];DBQ_c:\temp_sample.xls;驅動程式識別碼=790|
