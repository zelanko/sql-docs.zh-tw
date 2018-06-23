---
title: 使用 SQL Server Native Client 的時機 |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
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
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5e27d76ee3e8cf4c19ba9f0f36a2b0c710134c1d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135158"
---
# <a name="when-to-use-sql-server-native-client"></a>使用 SQL Server Native Client 的時機
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 是用來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料的一種技術。  如需不同的資料存取技術的討論，請參閱[資料存取技術藍圖](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 決定是否要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 當做應用程式的資料存取技術時，您應該考慮許多因素。  
  
 對於新的應用程式而言，如果您正在使用 Microsoft Visual C# 或 Visual Basic 等 Managed 程式語言，而且需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的新功能，則應該使用 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (屬於 .NET Framework 的一部分)。  
  
 如果您正在開發以 COM 為基礎的應用程式，而且需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所導入的新功能，則應該使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。 如果您不需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能，可以繼續使用 Windows Data Access Components (WDAC)。  
  
 對於現有的 OLE DB 和 ODBC 應用程式而言，主要的問題在於您是否需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能。 如果您有一個不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之新功能的完整應用程式，就可以繼續使用 WDAC。 但是，如果您需要存取這些新功能，例如[xml 資料型別](/sql/t-sql/xml/xml-transact-sql)，您應該使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 和 MDAC 都可使用資料列版本設定來支援讀取認可的交易隔離，但是只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 可支援快照集交易隔離  (在程式設計的詞彙中，含有資料列版本設定的讀取認可交易隔離與讀取認可的交易相同)。  
  
 如需有關之間的差異資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 與 MDAC，請參閱[更新至 SQL Server Native Client 應用程式從 MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC 使用說明主題](../native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 的使用說明主題](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
