---
title: "SQLDriverConnect （文字檔案驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 117b619b351e5a8c1e2c0865fe0ed6add5589ecb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect （文字檔案驅動程式）
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**可讓您連接至驅動程式，而不需要建立資料來源 (DSN)。  
  
 在連接字串的所有驅動程式支援下列關鍵字： **DSN**， **DBQ**，和**FIL**。  
  
 下表顯示最小的關鍵字，才能連接至每個驅動程式，並提供範例搭配使用的關鍵字/值組的**SQLDriverConnect**。 如需完整的 DRIVERID 值清單，請參閱[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。  
  
> [!NOTE]  
>  如果未指定文字驅動程式的 DBQ 或 DefaultDir，驅動程式會連接到目前的目錄。  
  
|驅動程式|所需的關鍵字|範例|  
|------------|-----------------------|--------------|  
|Text|驅動程式|Driver = {Microsoft 文字驅動程式 (*.txt;\*。csv)};DefaultDir = c:\temp|

