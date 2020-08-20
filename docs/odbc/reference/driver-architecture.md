---
description: 驅動程式架構
title: 驅動程式架構 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 530940cef233b8a6b6a3f5c0575dd154998126cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494611"
---
# <a name="driver-architecture"></a>驅動程式架構
驅動程式架構分為兩種類別，取決於處理 SQL 語句的軟體：  
  
-   以檔案**為基礎的驅動程式**驅動程式會直接存取實體資料。 在此情況下，驅動程式會當做驅動程式和資料來源;也就是說，它會處理 ODBC 呼叫和 SQL 語句。 例如，dBASE 驅動程式是以檔案為基礎的驅動程式，因為 dBASE 不提供驅動程式可使用的獨立資料庫引擎。 請務必注意，以檔案為基礎之驅動程式的開發人員必須撰寫自己的資料庫引擎。  
  
-   以**DBMS 為基礎的驅動程式**驅動程式會透過個別的資料庫引擎來存取實體資料。 在此情況下，驅動程式只會處理 ODBC 呼叫;它會將 SQL 語句傳遞至資料庫引擎進行處理。 例如，Oracle 驅動程式是以 DBMS 為基礎的驅動程式，因為 Oracle 具有驅動程式所使用的獨立資料庫引擎。 資料庫引擎所在的位置是並不重要。 它可以位於與驅動程式相同的電腦或網路上的其他電腦上;您甚至可以透過閘道來存取它。  
  
 驅動程式架構通常只對驅動程式寫入器很有趣;也就是說，驅動程式架構通常不會與應用程式產生任何差異。 不過，架構可能會影響應用程式是否可以使用 DBMS 特定的 SQL。 例如，Microsoft Access 提供獨立的資料庫引擎。 如果 Microsoft Access 驅動程式是以 DBMS 為基礎，它會透過此引擎存取資料，應用程式可以將 Microsoft Access-SQL 語句傳遞給引擎進行處理。  
  
 但是，如果是以檔案為基礎的驅動程式，也就是它包含可直接存取 Microsoft® Access .mdb 檔案的專屬引擎-任何將 Microsoft Access 特定 SQL 語句傳遞給引擎的嘗試，都可能會造成語法錯誤。 原因是專屬引擎可能只會執行 ODBC SQL。  
  
 此章節包含下列主題。  
  
-   [以檔案為基礎的驅動程式](../../odbc/reference/file-based-drivers.md)  
  
-   [以 DBMS 為基礎的驅動程式](../../odbc/reference/dbms-based-drivers.md)  
  
-   [網路範例](../../odbc/reference/network-example.md)  
  
-   [其他驅動程式架構](../../odbc/reference/other-driver-architectures.md)
