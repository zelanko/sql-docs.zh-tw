---
title: SQLDriverConnect （Access 驅動程式） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302909"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLDriverConnect**可讓您連接到驅動程式，而不需要建立資料來源（DSN）。  
  
 下列關鍵字在所有驅動程式的連接字串中都受到支援： **DSN**、 **DBQ**和**FIL**。  
  
 **UID**和**PWD**關鍵字也受到支援。  
  
 PWD 關鍵字不應包含任何特殊字元（請參閱**SQLGetInfo**傳回值中的 SQL_SPECIAL_CHARACTERS）。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供搭配**SQLDriverConnect**使用之關鍵字/值組的範例。 如需 DRIVERID 值的完整清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。  
  
|驅動程式|需要關鍵字|範例|  
|------------|-----------------------|--------------|  
|Microsoft Access|驅動程式，DBQ|驅動程式 = {Microsoft Access 驅動程式（* .mdb）};DBQ = c：\\\temp\\\sample.mdb|
