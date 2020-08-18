---
description: VARCHAR 資料行大小 (ODBC Driver for Oracle)
title: " (ODBC Driver for Oracle) 的 VARCHAR 資料行大小 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c490487f0edb15fe7d7165b79c4c5f1730a0dd22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449060"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 資料行大小 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 在 Oracle8 中，VARCHAR 資料行的大小上限從2000增加到4000個位元組。 Oracle 7.3. x 用戶端軟體無法系結超過2000個位元組的參數值。 因此，如果您建立的資料表具有大於2000個位元組的 VARCHAR 資料行，您將無法針對該資料表使用超過用戶端軟體2000位元組限制的資料來執行參數化插入、更新、刪除和查詢。 由於 ODBC Driver for Oracle 和 OLE DB Provider for Oracle 會使用參數化插入、更新、刪除和查詢，所以在此情況下，它們會回報 TNSNAMES.ORA-01026 錯誤。 Oracle 用戶端軟體所強制執行之限制內的資料將會運作。 若要避免這個2000位元組的限制，您必須將用戶端軟體升級至 Oracle8 (8.0.4.1.1 c 或更高版本的) 。
