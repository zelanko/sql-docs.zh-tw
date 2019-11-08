---
title: SQL Server Native Client 的元件 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a2dfe1dd9192277ebdf02017abae692dff30e2e1
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73772549"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client 的元件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 包含下列元件：  
  
|元件|說明|  
|---------------|-----------------|  
|sqlncli11.dll|包含所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 功能的動態連結程式庫 (DLL) 檔案。 這包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式。|  
|sqlnclir11.rll|隨附 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 程式庫的資源檔。|   
|sqlncli.h|包含使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 所需之所有新定義的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔。 此標頭檔會同時取代 odbcss.h 和 sqloledb.h 標頭檔。<br /><br /> 注意：您不能在相同的程式中參考 sqlncli 和 odbcss.h，但是只要先定義 sqloledb，就可以在同一個程式中參考 sqlncli 和 sqloledb。|  
|sqlncli11.lib|直接呼叫**bcp**公用程式函式所需的程式庫檔案，這些函式是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式的一部分。<br /><br /> 注意：如果您在程式碼中參考 sqlncli11 檔案，則必須確定 sqlncli11 檔案位於您的系統路徑中，以及使用您的應用程式之使用者的系統路徑中。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建立應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
