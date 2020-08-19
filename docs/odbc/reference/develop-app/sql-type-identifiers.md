---
description: SQL 類型識別碼
title: SQL 類型識別碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 211cfdbe7805bade2875723a1cb62a02b5c876d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424510"
---
# <a name="sql-type-identifiers"></a>SQL 類型識別碼
每個資料來源都會定義自己的 SQL 資料類型。 ODBC 會定義類型識別碼，並描述可能對應至每個類型識別碼之 SQL 資料類型的一般特性。 它是基礎資料來源中每個資料類型對應至 ODBC SQL 類型識別碼的驅動程式特定。  
  
 例如，SQL_CHAR 是具有固定長度的字元資料行類型識別碼，通常介於1到254個字元之間。 這些特性會對應到在許多 SQL 資料來源中找到的 CHAR 資料類型。 因此，當應用程式發現資料行的類型識別碼是 SQL_CHAR 時，它可以假設它可能會處理 CHAR 資料行。 不過，它仍應先檢查資料行的位元組長度，再假設它介於1到254個字元之間;例如，非 SQL 資料來源的驅動程式可能會將500個字元的固定長度字元資料行對應到 SQL_CHAR 或 SQL_LONGVARCHAR，因為兩者都不完全相符。  
  
 ODBC 定義各式各樣的 SQL 類型識別碼。 不過，驅動程式不需要使用這些識別碼。 相反地，它只會使用所需的識別碼來公開基礎資料來源所支援的 SQL 資料類型。 如果基礎資料來源支援的 SQL 資料類型不會對應到任何類型識別碼，驅動程式可以定義其他類型識別碼。 如需詳細資訊，請參閱 [驅動程式特定的資料類型、描述項類型、資訊類型、診斷類型與屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 如需 SQL 類型識別碼的完整說明，請參閱附錄 D：資料類型中的 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md) 。
