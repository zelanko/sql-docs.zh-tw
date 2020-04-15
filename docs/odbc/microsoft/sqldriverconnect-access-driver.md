---
title: SQLDriver連接(存取驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a679cbb16ece3f239b1d17daabc8a294b808287
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302909"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (Access 驅動程式)
> [!NOTE]  
>  本主題提供特定於訪問驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLDriverConnect**使您能夠連接到驅動程式,而無需創建資料源 (DSN)。  
  
 所有驅動程式的連接字串都支援以下關鍵字 **:DSN、DBQ****DBQ**和**FIL**。  
  
 也支援**UID**和**PWD**關鍵字。  
  
 PWD 關鍵字不應包含任何特殊字元(請參閱**SQLGetInfo**返回值中的SQL_SPECIAL_CHARACTERS)。  
  
 下表顯示了連接到每個驅動程式所需的最小關鍵字,並提供了**SQLDriverConnect**一起使用的關鍵字/值對的範例。 有關 DRIVERID 值的完整清單,請參考[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。  
  
|驅動程式|需要關鍵字|範例|  
|------------|-----------------------|--------------|  
|Microsoft Access|驅動程式,DBQ|驅動程式[微軟存取驅動程式 (*.mdb)];DBQ_c:\\\temp\\_sample.mdb|
