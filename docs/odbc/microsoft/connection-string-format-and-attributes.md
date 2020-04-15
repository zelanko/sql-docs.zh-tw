---
title: 連接字串格式與屬性 :微軟文件
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
ms.openlocfilehash: d95866976d2e83c058f83b3a0ae5e9a4e8888ed1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281148"
---
# <a name="connection-string-format-and-attributes"></a>連接字串格式和屬性
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 某些應用程式可能需要指定數據源連接資訊的連接字串,而不是使用對話方塊。 連接字串由許多屬性組成,這些屬性指定驅動程式如何連接到數據源。 屬性識別驅動程式在建立適當的數據源連接之前需要知道的特定資訊段。 每個驅動程式可能具有一組不同的屬性,但連接字串格式始終相同。 連接字串有以下格式:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Oracle 的 Microsoft ODBC 驅動程式支援驅動程式的第一個版本的連接字串格式,該`CONNECTSTRING`驅動`SERVER=`程式使用 = 而不是 。  
  
 如果要連接到支援 Windows 身份驗證的資料來源提供者,則應在連接字串`Trusted_Connection=yes`中指定 而不是使用者 ID 和密碼資訊。  
  
 如果不指定 UID、PWD、SERVER(或 CONNECTSTRING)和 DRIVER 屬性,則必須指定數據原始名稱。 但是,所有其他屬性都是可選的。 如果不指定屬性,該屬性預設為**ODBC 數據來源管理員**對話方塊的相關 DSN 選項卡中指定的屬性。 屬性值可能區分大小寫。  
  
 連接字串的屬性如下所示:  
  
|屬性|描述|預設值|  
|---------------|-----------------|-------------------|  
|DSN|**ODBC 資料來源管理員**對話方塊的驅動程式"選項卡中列出的數據源名稱。|""|  
|PWD|要存取的 Oracle 伺服器的密碼。 此驅動程式支援 Oracle 對密碼的限制。|""|  
|SERVER|要存取的 Oracle 伺服器的連接字串。|""|  
|UID|Oracle 伺服器使用者名稱。 根據您的系統,此屬性可能不是可選的 - 也就是說,出於安全目的,某些資料庫和表可能需要此屬性。<br /><br /> 使用"/"使用 Oracle 的作業系統身份驗證。|""|  
|緩衝區大小|提取列時使用的最佳緩衝區大小。<br /><br /> 驅動程式優化提取,以便從 Oracle 伺服器提取的行返回足夠的行來填充此大小的緩衝區。 如果獲取大量數據,則值越大,性能也會提高。|65535|  
|同義詞|當此值為 true (1)時,SQLColumn( ) API 呼叫將返回列資訊。 否則,SQLColumn( ) 僅返回表和檢視的列。 未設定此值時,Oracle 的 ODBC 驅動程式可提供更快的訪問。|1|  
|REMARKS|當此值為 true (1)時,驅動程式返回[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)結果集的備註列。 未設定此值時,Oracle 的 ODBC 驅動程式可提供更快的訪問。|0|  
|斯特德日周|為「天天」標量強制實施 ODBC 標準。 默認情況下,這已打開,但需要當地語系化版本的使用者可以更改行為以使用 Oracle 返回的任何內容。|1|  
|猜謎|指定驅動程式是否應返回**SQLDescribeCol**的*cbColDef*參數的非零值。 僅適用於沒有 Oracle 定義比例的欄,例如計算的數位列和定義為 NUMBER 的列,而不具有精度或比例。 當 Oracle 不提供該資訊時 **,SQLDescribeCol**調用返回 130 的精度。|0|  
  
 例如,使用 MyOracleServerOracle 伺服器和 Oracle 使用者 MyUserID 連線到 MyDataSource 資料來源的連接字串是:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 使用作業系統身份驗證與 MyOtherOracleServerOracle 伺服器連線到 MyOtherDataSource 資料來源的連接字串是:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
