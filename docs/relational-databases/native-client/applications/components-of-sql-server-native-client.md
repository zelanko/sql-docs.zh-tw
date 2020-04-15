---
title: SQL 伺服器本機客戶端的元件 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bae5a3871750791d3339e2b98b715ec3779d105d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302504"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client 的元件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 包含下列元件：  
  
|元件|描述|  
|---------------|-----------------|  
|sqlncli11.dll|包含所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 功能的動態連結程式庫 (DLL) 檔案。 這包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式。|  
|sqlnclir11.rll|隨附 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 程式庫的資源檔。|   
|sqlncli.h|包含使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 所需之所有新定義的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔。 此標頭檔會同時取代 odbcss.h 和 sqloledb.h 標頭檔。<br /><br /> 注意:您不能在同一程式中引用 sqlncli.h 和 odbcs.h,但只要首先定義 sqloledb.h,就可以在同一程式中引用 sqlncli.h 和 sqloledb.h。|  
|sqlncli11.lib|直接呼叫作為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式一部分的**bcp**實用程式函數所需的庫檔。<br /><br /> 注意:如果確實在程式設計代碼中引用 sqlncli11.lib 檔案,則需要確保 sqlncli11.dll 檔案位於系統路徑中,以及使用應用程式的使用者的系統路徑中。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建立應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
