---
description: SQLDriverConnect (Paradox 驅動程式)
title: SQLDriverConnect (Paradox 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b6bffe650bfc204660d7345b1bd5a051105fb5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421812"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLDriverConnect** 可讓您連接到驅動程式，而不需建立資料來源 (DSN) 。  
  
 所有驅動程式的連接字串都支援下列關鍵字： **DSN**、 **DBQ**和 **FIL**。  
  
 也支援 **PWD** 關鍵字。 PWD 關鍵字不應包含任何特殊字元 (請參閱 SQL_SPECIAL_CHARACTERS **SQLGetInfo** 傳回的值) 。  
  
 當使用者開啟受密碼保護的檔案之後，不允許其他使用者開啟相同的檔案。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供與 **SQLDriverConnect**搭配使用的關鍵字/值組範例。 如需 DRIVERID 值的完整清單，請參閱 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。  
  
> [!NOTE]  
>  如果未指定 Paradox 驅動程式的 DBQ 或 DefaultDir，驅動程式將會連接到目前的目錄。  
  
|驅動程式|必要關鍵字|範例|  
|------------|-----------------------|-------------|  
|悖論|驅動程式，DriverID|驅動程式 = {Microsoft Paradox 驅動程式 ( *. 資料庫 ) };DBQ = c：\temp; DriverID = 26|
