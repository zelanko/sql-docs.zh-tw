---
description: SQLDriverConnect (Access 驅動程式)
title: SQLDriverConnect (Access 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 52bbcbfa379be53ea24c150d2522242e85e61fea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449210"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLDriverConnect** 可讓您連接到驅動程式，而不需建立資料來源 (DSN) 。  
  
 所有驅動程式的連接字串都支援下列關鍵字： **DSN**、 **DBQ**和 **FIL**。  
  
 也支援 **UID** 和 **PWD** 關鍵字。  
  
 PWD 關鍵字不應包含任何特殊字元 (請參閱 SQL_SPECIAL_CHARACTERS **SQLGetInfo** 傳回的值) 。  
  
 下表顯示連接到每個驅動程式所需的最小關鍵字，並提供與 **SQLDriverConnect**搭配使用的關鍵字/值組範例。 如需 DRIVERID 值的完整清單，請參閱 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。  
  
|驅動程式|必要關鍵字|範例|  
|------------|-----------------------|--------------|  
|Microsoft Access|驅動程式，DBQ|Driver = {Microsoft Access Driver ( * .mdb) };DBQ = c： \\ \temp \\ \sample.mdb|
