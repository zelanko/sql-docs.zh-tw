---
title: SQLDriver連接(dBASE驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39d3d062ef8371ce37f812216cbb642d103eff98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302919"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供特定於 dBASE 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLDriverConnect**使您能夠連接到驅動程式,而無需創建資料源 (DSN)。  
  
 所有驅動程式的連接字串都支援以下關鍵字 **:DSN、DBQ****DBQ**和**FIL**。  
  
 使用 Paradox 驅動程式時,使用者打開受密碼保護的檔後,不允許其他使用者打開同一檔。  
  
 下表顯示了連接到每個驅動程式所需的最小關鍵字,並提供了**SQLDriverConnect**一起使用的關鍵字/值對的範例。 有關 DRIVERID 值的完整清單,請參考[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。  
  
> [!NOTE]  
>  如果未為 dBASEdriver 指定 DBQ 或 DefaultDir,則驅動程式將連接到當前目錄。  
  
|驅動程式|需要的關鍵字|範例|  
|------------|-----------------------|--------------|  
|dBASE|驅動程式,驅動程式識別碼|驅動程式[微軟 dBASE 驅動程式 (*.dbf)];DBQ_c:\temp;驅動程式識別碼=277|
