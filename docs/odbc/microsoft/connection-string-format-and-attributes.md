---
title: 連接字串格式和屬性 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 258391853e03879b6b970347c8ca3f6f2e0eacc9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connection-string-format-and-attributes"></a>連接字串格式和屬性
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 不使用對話方塊中，某些應用程式可能需要指定資料來源連接資訊的連接字串。 指定驅動程式如何連接至資料來源的屬性數目是由連接字串所組成。 屬性會識別特定的驅動程式必須知道才能做出適當的資料來源連接的資訊片段。 每個驅動程式可能會有一組不同的屬性，但連接字串格式一定是相同的。 連接字串具有下列格式：  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC Driver for Oracle 支援的驅動程式使用的第一個版本的連接字串格式`CONNECTSTRING`= 而不是`SERVER=`。  
  
 如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定`Trusted_Connection=yes`而不是在連接字串中的使用者識別碼和密碼資訊。  
  
 您必須指定資料來源名稱，如果您未指定 UID、 PWD、 伺服器 （或 CONNECTSTRING），以及驅動程式屬性。 不過，所有其他屬性是選擇性的。 如果您未指定屬性，該屬性會預設為相關 DSN 索引標籤中所指定**ODBC 資料來源管理員** 對話方塊。 此屬性值可能會區分大小寫。  
  
 連接字串屬性如下所示：  
  
|Attribute|Description|預設值|  
|---------------|-----------------|-------------------|  
|DSN|資料來源名稱列在 驅動程式 索引標籤的**ODBC 資料來源管理員** 對話方塊。|""|  
|PWD|您想要存取 Oracle 伺服器的密碼。 此驅動程式支援 Oracle 放到密碼的限制。|""|  
|SERVER|您想要存取 Oracle 伺服器的連接字串。|""|  
|UID|Oracle 伺服器的使用者名稱。 根據您的系統，此屬性可能不是選擇性，也就是特定的資料庫和資料表可能會需要這個屬性基於安全性考量。<br /><br /> 使用"/"使用 Oracle 的操作系統驗證。|""|  
|BUFFERSIZE|使用擷取資料行時，最佳的緩衝區大小。<br /><br /> 驅動程式會最佳化提取，以便在 Oracle 伺服器從一個提取都會傳回足夠的資料列，以填滿緩衝區大小。 較大的值通常會增加效能，如果您擷取大量資料。|65535|  
|SYNONYMCOLUMNS|當這個值為 true (1)、 SQLColumn （） API 呼叫傳回的資料行資訊。 否則，SQLColumn （） 傳回資料表和檢視表的資料的行。 未設定此值時，oracle ODBC 驅動程式提供存取速度。|1|  
|REMARKS|當這個值為 true (1)，驅動程式會傳回註解的資料行[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)結果集。 未設定此值時，oracle ODBC 驅動程式提供存取速度。|0|  
|StdDayOfWeek|會強制執行的 DAYOFWEEK 純量的 ODBC 標準。 依預設會開啟，但需要當地語系化的版本的使用者可以變更要使用 Oracle 所傳回的任何內容的行為。|1|  
|GuessTheColDef|指定驅動程式是否應該傳回非零的值*cbColDef*引數的**SQLDescribeCol**。 僅適用於資料行，其中有任何 Oracle 定義小數位數，例如計算數值資料行和資料行定義為數字，不含有效位數或小數位數。 A **SQLDescribeCol** Oracle 不提供該資訊時，呼叫傳回 130 之有效位數。|0|  
  
 例如，連接到使用 MyOracleServerOracle Server 和 Oracle 使用者 MyUserID MyDataSource 資料來源的連接字串會：  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 會連接到使用作業系統驗證和 MyOtherOracleServerOracle 伺服器 MyOtherDataSource 資料來源的連接字串：  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
