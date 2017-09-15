---
title: "VARCHAR 資料行大小 （oracle 的 ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57dcc53769c9b5ba80f5c949436f0b3eb2ce08b1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 資料行大小 （oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 在 Oracle8，VARCHAR 資料行的大小上限已經增加從 2000年到 4000 個位元組。 Oracle 7.3.x 用戶端軟體並沒有繫結的參數值超過 2000 個位元組的方式。 因此，如果您建立與超過 2000 個位元組的 VARCHAR 資料行的資料表，您將無法執行參數化的插入、 更新、 刪除和查詢的資料超過 2000年個位元組限制的用戶端軟體。 ODBC Driver for Oracle 和 Oracle OLE DB 提供者都使用參數化的插入、 更新、 刪除和查詢，因為它們會在此情況下報告 ORA-TUT1-LESSON1-STEP2 01026 錯誤。 將工作強制執行的 Oracle 用戶端軟體在限制範圍內的資料。 若要避免此 2000年個位元組限制，您必須升級用戶端軟體，為 Oracle8 (8.0.4.1.1c 或更高版本)。
