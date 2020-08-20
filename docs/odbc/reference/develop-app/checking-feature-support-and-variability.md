---
description: 檢查功能支援和變化性
title: 檢查功能支援和變化性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60fb6b39d7b2326a925aea40303ce52165cca8a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465910"
---
# <a name="checking-feature-support-and-variability"></a>檢查功能支援和變化性
為了檢查功能支援和變化性，應用程式通常會呼叫 **SQLGetInfo**、 **SQLGetFunctions**和 **SQLGetTypeInfo**。 驅動程式的 API 和 SQL 文法一致性層級是不錯的開始位置。 這些描述廣泛的功能支援層級。 然後，應用程式可以使用其他選項來呼叫 **SQLGetInfo** ，以判斷其所需功能的支援或變異數， **SQLGetFunctions** 以判斷是否支援所需的函式超過傳回的一致性層級，以及 **SQLGetTypeInfo** 判斷支援的 SQL 資料類型。  
  
 應用程式可以使用該屬性來呼叫 **SQLSetStmtAttr** 或 **SQLSetConnectAttr** ，以判斷是否支援語句或連接屬性。 如果函式傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則支援此屬性。如果它傳回 SQL_ERROR，且 SQLSTATE HYC00 (選用功能未實作為) ，則不支援此屬性。  
  
 應用程式也可以藉由呼叫 **SQLDrivers**，在連接到驅動程式之前判斷出有限數量的資訊。
