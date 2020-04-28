---
title: SQLDriverConnect （dBASE 驅動程式） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302919"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLDriverConnect**可讓您連接到驅動程式，而不需要建立資料來源（DSN）。  
  
 下列關鍵字在所有驅動程式的連接字串中都受到支援： **DSN**、 **DBQ**和**FIL**。  
  
 當使用 Paradox 驅動程式時，使用者開啟受密碼保護的檔案之後，不允許其他使用者開啟相同的檔案。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供搭配**SQLDriverConnect**使用之關鍵字/值組的範例。 如需 DRIVERID 值的完整清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。  
  
> [!NOTE]  
>  如果未指定 dBASEdriver 的 DBQ 或 DefaultDir，驅動程式將會連接到目前的目錄。  
  
|驅動程式|需要關鍵字|範例|  
|------------|-----------------------|--------------|  
|dBASE|驅動程式，DriverID|驅動程式 = {Microsoft dBASE 驅動程式（* .dbf）};DBQ = c：\temp;DriverID = 277|
