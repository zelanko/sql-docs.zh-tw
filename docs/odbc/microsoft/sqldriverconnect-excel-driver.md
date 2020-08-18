---
description: SQLDriverConnect (Excel 驅動程式)
title: SQLDriverConnect (Excel 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 6320033d83e9b46c3567b3bf0b845144dbe9250e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449190"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLDriverConnect** 可讓您連接到驅動程式，而不需建立資料來源 (DSN) 。  
  
 所有驅動程式的連接字串都支援下列關鍵字： **DSN**、 **DBQ**和 **FIL**。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供與 **SQLDriverConnect**搭配使用的關鍵字/值組範例。 如需 DRIVERID 值的完整清單，請參閱 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。  
  
> [!NOTE]  
>  如果未指定 Microsoft Excel 3.0 或4.0 驅動程式的 DBQ 或 DefaultDir，驅動程式將會連接到目前的目錄。  
  
|驅動程式|必要關鍵字|範例|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 或4。0|驅動程式，DriverID|Driver = {Microsoft Excel Driver ( * .xls) };DBQ = c：\temp;DriverID = 278|  
|Microsoft Excel 5.0/7。0|Driver、DriverID、DBQ|Driver = {Microsoft Excel Driver ( * .xls) };DBQ =c:\temp\sample.xls;DriverID = 22|  
|Microsoft Excel 97 和更新版本|Driver、DriverID、DBQ|Driver = {Microsoft Excel Driver ( * .xls) };DBQ =c:\temp\sample.xls;DriverID = 790|
