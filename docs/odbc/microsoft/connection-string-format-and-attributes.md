---
description: 連接字串格式和屬性
title: 連接字串格式和屬性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53efb4dd010913029185f0cbf27f0991f34815fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412930"
---
# <a name="connection-string-format-and-attributes"></a>連接字串格式和屬性
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 有些應用程式可能需要指定資料來源連接資訊的連接字串，而不是使用對話方塊。 連接字串是由數個屬性所組成，可指定驅動程式連接至資料來源的方式。 屬性會識別驅動程式必須知道的特定資訊，才能進行適當的資料來源連接。 每個驅動程式可能會有不同的屬性集，但連接字串格式一律相同。 連接字串的格式如下：  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC Driver for Oracle 支援驅動程式第一個版本的連接字串格式，它使用 `CONNECTSTRING` = 而不是 `SERVER=` 。  
  
 如果您要連接到支援 Windows 驗證的資料來源提供者，您應該 `Trusted_Connection=yes` 在連接字串中指定，而不是使用者識別碼和密碼資訊。  
  
 如果您未指定 UID、PWD、伺服器 (或 CONNECTSTRING) 和驅動程式屬性，則必須指定資料來源名稱。 不過，其他所有屬性都是選擇性的。 如果您沒有指定屬性，該屬性會預設為 [ **ODBC 資料來源管理員** ] 對話方塊的 [相關 DSN] 索引標籤中指定的屬性。 屬性值可能會區分大小寫。  
  
 連接字串的屬性如下所示：  
  
|屬性|描述|預設值|  
|---------------|-----------------|-------------------|  
|DSN|在 [ **ODBC 資料來源管理員** ] 對話方塊的 [驅動程式] 索引標籤中列出的資料來源名稱。|""|  
|PWD|您要存取的 Oracle 伺服器的密碼。 此驅動程式支援 Oracle 放置密碼的限制。|""|  
|SERVER|您要存取的 Oracle 伺服器的連接字串。|""|  
|UID|Oracle 伺服器的使用者名稱。 視您的系統而定，此屬性可能不是選擇性的，也就是某些資料庫和資料表基於安全性目的可能需要此屬性。<br /><br /> 使用 "/" 可使用 Oracle 的作業系統驗證。|""|  
|BUFFERSIZE|提取資料行時所使用的最佳緩衝區大小。<br /><br /> 驅動程式會優化提取，讓來自 Oracle 伺服器的一個提取會傳回足夠的資料列，以填滿此大小的緩衝區。 如果您提取大量資料，較大的值通常會提高效能。|65535|  
|SYNONYMCOLUMNS|當此值為 true 時 (1) ，SQLColumn ( ) API 呼叫會傳回資料行資訊。 否則，SQLColumn ( ) 只會傳回資料表和 views 的資料行。 當未設定此值時，ODBC Driver for Oracle 可提供更快速的存取。|1|  
|REMARKS|當此值為 true 時 (1) ，驅動程式會傳回 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 結果集的備註資料行。 當未設定此值時，ODBC Driver for Oracle 可提供更快速的存取。|0|  
|StdDayOfWeek|強制執行 DAYOFWEEK 純量的 ODBC 標準。 預設會開啟此功能，但需要當地語系化版本的使用者可以將行為變更為使用 Oracle 傳回的任何內容。|1|  
|GuessTheColDef|指定驅動程式是否應針對**SQLDescribeCol**的*cbColDef*引數傳回非零值。 只適用于沒有 Oracle 定義之小數位數的資料行，例如計算的數值資料行和資料行，定義為沒有有效位數或小數位數的數位。 當 Oracle 未提供該資訊時， **SQLDescribeCol** 呼叫會傳回130的有效位數。|0|  
  
 例如，使用 MyOracleServerOracle 伺服器和 Oracle 使用者 MyUserID 連接到 MyDataSource 資料來源的連接字串會是：  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 使用作業系統驗證和 MyOtherOracleServerOracle 伺服器連接到 MyOtherDataSource 資料來源的連接字串將會是：  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
