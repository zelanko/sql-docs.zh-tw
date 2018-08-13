---
title: 準備命令 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- prepared statements [SQL Server Native Client]
- commands [OLE DB]
- command preparation [SQL Server Native Client]
ms.assetid: 09ec0c6c-0a44-4766-b9b7-5092f676ee54
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 096aff783be598522569d0963679080971d776ed
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39532968"
---
# <a name="preparing-commands"></a>準備命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援針對單一命令的最佳化多次執行進行命令準備。不過，命令準備會產生負擔，而且取用者不需要準備命令，即可多次執行命令。 一般而言，如果某個命令將執行三次以上，您就應該準備此命令。  
  
 基於效能的考量，命令準備會延遲到執行命令為止。 這是預設行為。 在執行命令或執行中繼屬性作業之前，無法得知正在準備之命令中的任何錯誤。 將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 屬性 SSPROP_DEFERPREPARE 設定為 FALSE 可以關閉此預設行為。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，直接執行命令 (但不先準備命令) 時，系統會建立並快取執行計畫。 如果再次執行了 SQL 陳述式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會具有高效率演算法，可比對新的陳述式與快取中的現有執行計畫，然後針對該陳述式重複使用此執行計畫。  
  
 若為準備的命令，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對準備和執行命令陳述式提供原生支援。 當您準備陳述式時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立執行計畫、快取此計畫，並且將此執行計畫的控制代碼傳回給提供者。 然後，提供者會使用此控制代碼來重複執行陳述式。 此時，系統不會建立任何預存程序。 因為此控制代碼會直接識別 SQL 陳述式的執行計畫，而非比對陳述式與快取中的執行計畫 (如同直接執行的情況)，所以如果您知道陳述式將執行許多次，準備陳述式會比直接執行更有效率。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，準備的陳述式無法用來建立暫存物件，而且無法參考建立暫存物件 (例如暫存資料表) 的系統預存程序。 這些程序必須直接執行。  
  
 您永遠都不應該準備某些命令。 例如，您不應該準備指定預存程序執行或針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序建立包含無效文字的命令。  
  
 如果建立了暫存預存程序，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會執行此暫存預存程序，並傳回結果 (如同執行陳述式本身一樣)。  
  
 暫存預存程序建立是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者特有的初始化屬性 SSPROP_INIT_USEPROCFORPREP 所控制。 如果屬性值為 SSPROPVAL_USEPROCFORPREP_ON 或 SSPROPVAL_USEPROCFORPREP_ON_DROP，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會在準備命令時嘗試建立預存程序。 如果應用程式使用者具有足夠的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 權限，預存程序建立就會成功。  
  
 若為不常中斷連接的取用者，建立暫存預存程序可能會需要 **tempdb** (在其中建立暫存物件的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫) 的大量資源。 如果 SSPROP_INIT_USEPROCFORPREP 的值為 SSPROPVAL_USEPROCFORPREP_ ON，只有當建立此命令的工作階段中斷與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連接時，才會卸除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者所建立的暫存預存程序。 如果該連接是針對資料來源初始化所建立的預設連接，只有當資料來源成為未初始化時，才會卸除暫存預存程序。  
  
 如果 SSPROP_INIT_USEPROCFORPREP 的值為 SSPROPVAL_USEPROCFORPREP_ON_DROP，發生下列其中一種狀況時，就會卸除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的暫存預存程序：  
  
-   取用者使用 **ICommandText::SetCommandText** 來表示新的命令。  
  
-   取用者使用 **ICommandPrepare::Unprepare** 來表示它不再需要命令文字。  
  
-   取用者使用暫存預存程序來釋放命令物件的所有參考。  
  
 命令物件最多在 **tempdb** 中具有一個暫存預存程序。 任何現有的暫存預存程序都代表特定命令物件的目前命令文字。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
