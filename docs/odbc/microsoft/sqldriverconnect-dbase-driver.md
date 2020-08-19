---
description: SQLDriverConnect (dBASE 驅動程式)
title: SQLDriverConnect (dBASE 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: e15925b52c096acb1a1021c1a2f968c0863eacf0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449200"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLDriverConnect** 可讓您連接到驅動程式，而不需建立資料來源 (DSN) 。  
  
 所有驅動程式的連接字串都支援下列關鍵字： **DSN**、 **DBQ**和 **FIL**。  
  
 使用 Paradox 驅動程式時，使用者開啟受密碼保護的檔案之後，不允許其他使用者開啟相同的檔案。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供與 **SQLDriverConnect**搭配使用的關鍵字/值組範例。 如需 DRIVERID 值的完整清單，請參閱 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。  
  
> [!NOTE]  
>  如果未指定 dBASEdriver 的 DBQ 或 DefaultDir，驅動程式將會連接到目前的目錄。  
  
|驅動程式|必要關鍵字|範例|  
|------------|-----------------------|--------------|  
|dBASE|驅動程式，DriverID|Driver = {Microsoft dBASE Driver ( * .dbf) };DBQ = c：\temp;DriverID = 277|
