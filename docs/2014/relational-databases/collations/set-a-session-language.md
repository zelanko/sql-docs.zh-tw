---
title: 設定工作階段語言 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], international considerations
- globalization [SQL Server], sessions
- time [SQL Server]
- sessions [SQL Server], languages
- international considerations [SQL Server], sessions
- dates [SQL Server], session languages
- global considerations [SQL Server], sessions
- client-side session language
- time [SQL Server], session languages
- messages [SQL Server], international considerations
- server-side session language
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf4eb1d7595d16369a0355562f090b746a4203ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62918943"
---
# <a name="set-a-session-language"></a>設定工作階段語言
  工作階段語言可根據語言和文化喜好設定，用來設定在伺服器顯示下列元素的方式：  
  
-   錯誤訊息與其他系統訊息所使用的語言。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援所有系統錯誤字串及訊息的多個複本，而支援語言即為所提供之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語言版本的所有語言。 您可以利用 [sys.messages](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages) 目錄檢視來檢視這些訊息。 在您安裝當地語系化版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，會將這些系統訊息翻譯成您所安裝的語言版本。 依預設，您也會取得美國英文版的這些訊息。 此外，您也可以使用 [sp_addmessage](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)，新增以特定語言顯示的使用者自訂訊息。  
  
-   日期和時間資料的格式。  
  
-   星期日期和月份的名稱，其中包括縮寫。  
  
-   星期的第一天。  
  
-   貨幣資料。  
  
 工作階段設定可以使用 33 種語言。 如需語言的清單，請參閱＜ [sys.syslanguages](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql)＞。  
  
## <a name="setting-the-session-language-from-the-server"></a>從伺服器設定工作階段語言  
 若要從伺服器端設定工作階段語言，請使用 [SET LANGUAGE](/sql/t-sql/statements/set-language-transact-sql)。  
  
## <a name="setting-the-session-language-from-the-client"></a>從用戶端設定工作階段語言  
 您可以利用 OLE DB、ODBC 或 ADO.NET，在用戶端設定工作階段語言。 如果是 OLE DB，請使用 SSPROP_INIT_CURRENTLANGUAGE 屬性。 如需詳細資訊，請參閱 [初始化和授權屬性](../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
 如果是 ODBC，請使用 Language 關鍵字。 如需詳細資訊，請參閱 [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)。  
  
 如果是 ADO.NET，請使用 **ConnectionString** 物件的 **Current Language** 參數。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC) 軟體開發套件 (SDK) 文件集。  
  
  
