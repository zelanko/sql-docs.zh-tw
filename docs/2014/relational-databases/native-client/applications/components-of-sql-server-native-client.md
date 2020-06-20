---
title: SQL Server Native Client 的元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: rothja
ms.author: jroth
ms.openlocfilehash: 32438b9fb5473d9251acd0aceddb46db373f3548
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85017646"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client 的元件
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 包含下列元件：  
  
|元件|描述|  
|---------------|-----------------|  
|sqlncli11.dll|包含所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 功能的動態連結程式庫 (DLL) 檔案。 這包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式。|  
|sqlnclir11.rll|隨附 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 程式庫的資源檔。|  
|s10ch_sqlncli.chm|記載如何使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料來源的資料來源精靈說明檔。|  
|sqlncli.h|包含使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 所需之所有新定義的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔。 此標頭檔會同時取代 odbcss.h 和 sqloledb.h 標頭檔。 **注意：** 您不能在相同的程式中參考 sqlncli 和 odbcss.h，但是只要先定義 sqloledb，就可以在同一個程式中參考 sqlncli 和 sqloledb。|  
|sqlncli11.lib|直接呼叫屬於**bcp** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式一部分之 bcp 公用程式函式所需的程式庫檔案。 **注意：** 如果您在程式碼中參考 sqlncli11 檔案，您必須確定 sqlncli11.dll 檔案位於您的系統路徑中，以及使用您的應用程式之使用者的系統路徑中。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](building-applications-with-sql-server-native-client.md)  
  
  
