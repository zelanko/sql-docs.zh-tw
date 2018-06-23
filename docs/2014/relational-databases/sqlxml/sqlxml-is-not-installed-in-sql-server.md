---
title: SQLXML 不會安裝在 SQL Server |Microsoft 文件
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
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fc997b5230d86a12169ee1ca8fd8c294ad09a048
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036522"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML 不會安裝在 SQL Server 中
  在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前，SQLXML 4.0 隨附於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而且是所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本 ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 除外) 之預設安裝的一部分。 不過，從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已不再包含最新版 SQLXML (SQLXML 4.0 SP1)。 若要使用時安裝 SQLXML 4.0 SP1，下載從[SQLXML SP1 的安裝位置](http://www.microsoft.com/download/details.aspx?id=3522)。  
  
 如果某個應用程式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上執行而且需要 SQLXML 4.0，但是電腦並沒有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，您就必須下載並安裝 SQLXML 4.0 SP1。  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>使用 SQLOLEDB 和 SQL Server Native Client OLE DB Provider 的 SQLXML 4.0 SP1 行為以及新的資料類型  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了下列資料類型，而這些是使用 SQLXML 之開發人員可能會想要使用的資料類型：  
  
-   `Date`  
  
-   `Time`  
  
-   `DateTime2`  
  
-   `DateTimeOffset`  
  
 使用 SQLXML 4.0 SP1 搭配 SQLOLEDB (來自 Windows Data Access Components，之前稱為 Microsoft Data Access Components) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB (來自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) 時，這些新的類型將會針對開發人員顯示成字串。 搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者 11.0 使用時，SQLXML 4.0 SP1 會將這四個新的資料類型啟用成內建的純量類型。 在您下載 SQLXML 4.0 SP1 之前，將這些類型對應至非字串類型可能會導致某些資料遭截斷。 例如，對應`DateTime2`至`xsd:date`會導致資料截斷成[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]`DateTime`精確度為 3.33 毫秒。  
  
## <a name="see-also"></a>另請參閱  
 [SQLXML 4.0 程式設計概念](sqlxml-4-0-programming-concepts.md)  
  
  