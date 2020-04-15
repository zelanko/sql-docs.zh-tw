---
title: SQLDriver連接(文字檔案驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2768669b7dbb2066de0acedd5711911be0eac8fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307099"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (文字檔驅動程式)
> [!NOTE]  
>  本主題提供特定於文本檔驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLDriverConnect**使您能夠連接到驅動程式,而無需創建資料源 (DSN)。  
  
 所有驅動程式的連接字串都支援以下關鍵字 **:DSN、DBQ****DBQ**和**FIL**。  
  
 下表顯示了連接到每個驅動程式所需的最小關鍵字,並提供了**SQLDriverConnect**一起使用的關鍵字/值對的範例。 有關 DRIVERID 值的完整清單,請參考[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。  
  
> [!NOTE]  
>  如果未為文本驅動程式指定 DBQ 或 DefaultDir,則驅動程式將連接到當前目錄。  
  
|驅動程式|需要的關鍵字|範例|  
|------------|-----------------------|--------------|  
|Text|驅動程式|驅動程式\微軟文字驅動程式 (*.txt;\*.csv)*;預設 Dir_c:\temp|
