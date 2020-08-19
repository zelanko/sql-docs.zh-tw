---
description: SQLAllocConnect (Visual FoxPro ODBC Driver)
title: SQLAllocConnect (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 70d48b12-def5-475c-b8e1-654a55fdfe0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 548d8f1b0c4679f8cbfe8e5af39cfcf592087bc8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483401"
---
# <a name="sqlallocconnect-visual-foxpro-odbc-driver"></a>SQLAllocConnect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：核心層級  
  
 在*henv*所識別的環境內，為連接控制碼*hdbc*配置記憶體。 當呼叫[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)、 **SQLBrowseConnect**或[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)時，驅動程式管理員會處理此呼叫，並呼叫驅動程式的**SQLAllocConnect** 。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLAllocConnect](../../odbc/reference/syntax/sqlallocconnect-function.md) 。
