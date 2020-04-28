---
title: SQLAllocConnect （Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: 6e5fa95bb958431f717c073673e0b4ad93056e62
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300661"
---
# <a name="sqlallocconnect-visual-foxpro-odbc-driver"></a>SQLAllocConnect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：核心層級  
  
 在*henv*所識別的環境中，配置連接控制碼*hdbc*的記憶體。 驅動程式管理員會處理此呼叫，並在每次呼叫[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)、 **SQLBrowseConnect**或[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)時呼叫驅動程式的**SQLAllocConnect** 。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLAllocConnect](../../odbc/reference/syntax/sqlallocconnect-function.md) 。
