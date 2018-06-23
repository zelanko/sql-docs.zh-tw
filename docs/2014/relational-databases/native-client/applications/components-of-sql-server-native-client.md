---
title: SQL Server Native Client 的元件 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c1a53fe3338f7b987bdf2b26312d634964f3587e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031417"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client 的元件
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 包含下列元件：  
  
|元件|描述|  
|---------------|-----------------|  
|sqlncli11.dll|包含所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 功能的動態連結程式庫 (DLL) 檔案。 這包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式。|  
|sqlnclir11.rll|隨附 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 程式庫的資源檔。|  
|s10ch_sqlncli.chm|記載如何使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料來源的資料來源精靈說明檔。|  
|sqlncli.h|包含使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 所需之所有新定義的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭檔。 此標頭檔會同時取代 odbcss.h 和 sqloledb.h 標頭檔。 **注意：** 您無法參考 sqlncli.h 和 odbcss.h 中相同的程式，但您只要先定義 sqloledb.h 可以參考 sqlncli.h 和 sqloledb.h 相同程式中的。|  
|sqlncli11.lib|需要直接呼叫的程式庫檔案**bcp**屬於公用程式函式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式。 **注意：** 如果您在程式碼中參考 sqlncli11.lib 檔，您必須先確認 sqlncli11.dll 檔位於您的系統路徑，以及讓使用者的系統路徑的應用程式使用。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](building-applications-with-sql-server-native-client.md)  
  
  