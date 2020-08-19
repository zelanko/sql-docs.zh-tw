---
description: SQLDriverConnect (文字檔驅動程式)
title: SQLDriverConnect (文字檔驅動程式) |Microsoft Docs
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
ms.openlocfilehash: c2eb5c35e9f6ae56caa3c6e4ca7473defe3b8bc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421802"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLDriverConnect** 可讓您連接到驅動程式，而不需建立資料來源 (DSN) 。  
  
 所有驅動程式的連接字串都支援下列關鍵字： **DSN**、 **DBQ**和 **FIL**。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供與 **SQLDriverConnect**搭配使用的關鍵字/值組範例。 如需 DRIVERID 值的完整清單，請參閱 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。  
  
> [!NOTE]  
>  如果未指定文字驅動程式的 DBQ 或 DefaultDir，驅動程式將會連接到目前的目錄。  
  
|驅動程式|必要關鍵字|範例|  
|------------|-----------------------|--------------|  
|Text|驅動程式|Driver = {Microsoft Text Driver ( * .txt; \* 。csv) };DefaultDir = c：\temp|
