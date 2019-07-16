---
title: 使用 SQL Server Native Client 標頭和程式庫檔案 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header files [SQL Server Native Client]
- SQLNCLI, header files
- OLE DB, header files
- library files [SQL Server Native Client]
- SQL Server Native Client, header files
- data access [SQL Server Native Client], header files
- SQL Server Native Client ODBC driver,header files
- data access [SQL Server Native Client], library files
- SQL Server Native Client, library files
- ODBC applications, header files
- SQLNCLI, library files
ms.assetid: 69889a98-7740-4667-aecd-adfc0b37f6f0
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01cfd9fe1aba63e5b63c6878d0332bd3a4a8eaff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987541"
---
# <a name="using-the-sql-server-native-client-header-and-library-files"></a>使用 SQL Server Native Client 標頭檔與程式庫檔案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔與程式庫檔案會與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一起安裝。 開發應用程式時，將開發所需的所有檔案複製並安裝到您的開發環境相當重要。 如需有關安裝及轉散發[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，請參閱[安裝 SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔和程式庫檔案會安裝到下列位置：  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\110\SDK  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔 (sqlncli.h) 可用於將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 資料存取功能加入到您的自訂應用程式中。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔包含使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中所導入之新功能所需的所有定義、屬性 (Attribute)、屬性 (Property) 與介面。  
  
 除了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔之外，還包含一個 sqlncli11.lib 程式庫檔，這是適用於 ODBC 之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製程式 (BCP) 功能的匯出程式庫。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔與搭配 Microsoft Data Access Components (MDAC) 所使用的 sqloledb.h 和 odbcss.h 標頭檔具回溯相容性，但是不包含適用於 SQLOLEDB 的 CLSID (適用於 MDAC 隨附之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 OLE DB 提供者) 或適用於 XML 功能的符號 (不受 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 所支援)。  
  
 ODBC 應用程式在相同的程式中，無法參考 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭 (sqlncli.h) 和 odbcss.h。 即使您不使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中所導入的任何功能，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔也會就地使用舊版的 odbcss.h。  
  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的 OLE DB 應用程式僅需要參考 sqlncli.h。 如果應用程式同時使用 MDAC (SQLOLEDB) 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，則可以同時參考 sqloledb.h 和 sqlncli.h，但是必須先參考 sqloledb.h。  
  
## <a name="using-the-sql-server-native-client-header-file"></a>使用 SQL Server Native Client 標頭檔  
 若要使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 標頭檔，您必須使用**包括**陳述式併入您的 C /C++程式碼。 下列章節描述如何同時針對 OLE DB 和 ODBC 應用程式執行此動作。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔和程式庫檔案僅能使用 Visual Studio C++ 2002 或更新版本編譯。  
  
### <a name="ole-db"></a>OLE DB  
 透過下列幾行程式碼，在 OLE DB 應用程式中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔：  
  
```  
#define _SQLNCLI_OLEDB_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  如果應用程式同時使用 OLE DB 和 ODBC API，以上顯示的第一行程式碼應該省略。 此外，如果應用程式**包括**sqloledb.h，陳述式**包含**用於 sqlncli.h 的陳述式必須緊跟在後。  
  
 透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 建立資料來源的連接時，請使用 "SQLNCLI11" 當做提供者名稱字串。  
  
### <a name="odbc"></a>ODBC  
 透過下列幾行程式碼，在 ODBC 應用程式中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔：  
  
```  
#define _SQLNCLI_ODBC_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  如果應用程式同時使用 OLE DB 和 ODBC API，以上顯示的第一行程式碼應該省略。 此外，如果應用程式有適用於 odbcss.h 的 `#include` 陳述式，則必須移除該陳述式。  
  
 透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 建立資料來源的連接時，請使用 "SQL Server Native Client 11.0" 當做驅動程式名稱字串。  
  
## <a name="component-names-and-properties-by-version"></a>依版本排列的元件名稱和屬性  
  
|屬性|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 10.0<br /><br /> SQL Server 2008|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]|MDAC|  
|--------------|--------------------------------------------------|-------------------------------------------------------|---------------------------------------------------------------|----------|  
|ODBC 驅動程式名稱|SQL Native Client|SQL Server Native Client 10.0|SQL Server Native Client 11.0|[SQL Server]|  
|ODBC 標頭檔名稱|Sqlncli.h|Sqlncli.h|Sqlncli.h|Odbcss.h|  
|ODBC 驅動程式 DLL|Sqlncli.dll|Sqlncl10.dll|Sqlncl11.dll|sqlsrv32.dll|  
|適用於 BCP API 的 ODBC 程式庫檔|Sqlncli.lib|Sqlncli10.lib|Sqlncli11.lib|Odbcbcp.lib|  
|適用於 BCP API 的 ODBC DLL|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Odbcbcp.dll|  
|OLE DB PROGID|SQLNCLI|SQLNCLI10|SQLNCLI11|SQLOLEDB|  
|OLE DB 標頭檔名稱|Sqlncli.h|Sqlncli.h|Sqlncli.h|Sqloledb.h|  
|OLE DB 提供者 DLL|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Sqloledb.dll|  
  
 sqlncli.h 可透過 SQLNCLI_VER 巨集來支援多個版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 根據預設，SQLNCLI_VER 預設為最新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 若要建立使用 sqlncli10.dll 而非 sqlncli11.dll 的應用程式，請將 SQLNCLI_VER 設定為 10。  
  
## <a name="static-linking-and-bcp-functions"></a>靜態連結與 BCP 函數  
 當應用程式使用 BCP 函數時，應用程式最好在連接字串中指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  
  
 例如，如果您使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 以及 \Program Files\Microsoft SQL Server\110\SDK 中的相關程式庫檔案 (sqlncli11.lib) 和標頭檔 (sqlncli.h) 編譯應用程式，請務必在連接字串中指定 (使用 ODBC 當做範例) "DRIVER={SQL Server Native Client 11.0}"。  
  
 如需詳細資訊，請參閱 < 執行[執行大量複製作業](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
