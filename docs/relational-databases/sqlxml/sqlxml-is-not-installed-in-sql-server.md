---
description: SQLXML 不會安裝在 SQL Server 中
title: SQLXML 不會安裝在 SQL Server 中
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3c588a22c8a55419fac480ed3e38186c37ee148
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97429584"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML 不會安裝在 SQL Server 中
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前，SQLXML 4.0 隨附於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而且是所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本 ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 除外) 之預設安裝的一部分。 不過，從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已不再包含最新版 SQLXML (SQLXML 4.0 SP1)。 若要安裝 SQLXML 4.0 SP1，請從 [sqlxml 4.0 sp1 的安裝位置](https://www.microsoft.com/download/details.aspx?id=30403)下載此 sp1。  
  
 如果應用程式在上執行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而且需要 sqlxml 4.0，您必須下載並安裝 sqlxml 4.0 SP1。  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>使用 SQLOLEDB 和 SQL Server Native Client OLE DB Provider 的 SQLXML 4.0 SP1 行為以及新的資料類型  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引進了下列資料類型，這些資料類型的開發人員可能會想要使用 SQLXML：  
  
-   **日期**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 使用具有 SQLOLEDB 或 Native Client OLE DB 的 SQLXML 4.0 SP1 時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，這些類型會以字串的形式出現給開發人員。 當與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 或更新版本搭配使用時，SQLXML 4.0 SP1 會將這四種新的資料類型啟用成內建的純量類型。 在您下載 SQLXML 4.0 SP1 之前，將這些類型對應至非字串類型可能會導致某些資料遭截斷。 例如，將 **DateTime2** 對應至 **xsd： date** 會導致資料截斷為3.33 毫秒的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **日期時間** 有效位數。  
  
## <a name="see-also"></a>另請參閱  
 [SQLXML 4.0 程式設計概念](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
