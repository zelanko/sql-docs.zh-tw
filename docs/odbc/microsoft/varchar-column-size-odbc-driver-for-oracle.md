---
title: VARCHAR 資料行大小 (ODBC Driver for Oracle) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db2871324f92ef6d84a8bf8313db105489100a96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847566"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 資料行大小 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 在 Oracle8，VARCHAR 資料行的大小上限已增加從 2000年到 4000 個位元組。 Oracle 7.3.x 用戶端軟體便無法繫結參數值超過 2000 個位元組。 因此，如果您建立與超過 2000 個位元組的 VARCHAR 資料行的資料表，您將無法執行參數化的插入、 更新、 刪除和查詢它與超過 2000年個位元組限制的用戶端軟體的資料。 ODBC Driver for Oracle 和 OLE DB Provider for Oracle 都使用參數化的插入、 更新、 刪除和查詢，因為它們會在此情況下報告 ORA 01026 錯誤。 強制執行的 Oracle 用戶端軟體在限制範圍內的資料將會運作。 若要避免此 2000年個位元組限制，您必須升級您的用戶端軟體，為 Oracle8 (8.0.4.1.1c 或更高版本)。
