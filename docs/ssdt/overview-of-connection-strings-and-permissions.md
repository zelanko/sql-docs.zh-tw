---
title: 連接字串和權限概觀 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ceff114e-a738-46ad-9785-b6647a2247f9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 413d6ad71b70cc4ddca8205589d25e224bbcad76
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102025"
---
# <a name="overview-of-connection-strings-and-permissions"></a>連接字串和權限概觀
若要執行 SQL Server 單元測試，您必須使用一個或兩個特定連接字串來連接到資料庫伺服器。 每一個連接字串都代表具有特定權限的帳戶 (如果您要在測試中的特定指令碼執行某個工作或一組工作，必須擁有該帳戶)。 您可以在 [SQL Server 測試組態] 對話方塊中指定這些字串，或是手動為測試專案編輯 app.config 檔案來加以指定。  
  
## <a name="connection-strings"></a>連接字串  
您可以在 [SQL Server 測試組態] 對話方塊中，為以下的每一個帳戶指定連接字串。  
  
> [!NOTE]  
> 只有當您使用 SQL Server 驗證時，執行內容和授權的內容才會不同。 如果您是使用 Windows 驗證，兩個連接字串會使用相同的認證。  
  
-   執行內容 (必要) - 用來執行「測試指令碼」(Test Script) 的使用者帳戶。 這個連接字串應該具有您預期使用者所具備的相同認證， 這一點非常重要，因為這樣可確保適當的權限已經套用到資料庫。 如需詳細資訊，請參閱[如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)。  
  
    在測試專案的 app.config 檔案中，這就是 `ExecutionContext` 元素。  
  
-   授權的內容 (選用) - 相同資料庫上具有執行測試前動作、測試後動作、TestInitialize 和 TestCleanup 指令碼之較高權限的帳戶。 這些指令碼會設定資料庫狀態，而且如果是測試後動作，也可以用來驗證資料庫中的物件。 這個連接字串也可用來部署資料庫變更及產生資料。  
  
    在測試專案的 app.config 檔案中，這就是 `PrivilegedContext` 元素。 如果 SQL Server 單元測試只會執行測試指令碼，您就不需要指定授權的內容。  
  
您在專案組態對話方塊中所指定的字串會儲存在測試專案的 app.config 檔案中。 您也可以直接編輯這個檔案並重建專案，然後新的值就會出現在此對話方塊中。  
  
## <a name="windows-authentication-versus-sql-server-authentication"></a>Windows 驗證和 SQL Server 驗證  
在指定連接字串時，您必須在使用 Windows 驗證和 SQL 驗證之間做出選擇。 選擇 Windows 驗證的其中一個理由是此驗證方式對小組使用測試的支援優於 SQL Server 驗證。 如果您選擇 SQL Server 驗證，則會根據使用者認證將連接字串加密 (使用資料保護 API (DPAPI))。 這表示，此測試專案中的測試將只為您執行，如果是在您簽入它們之後透過原始檔控制系統取得測試的團隊成員就無法執行。 若要執行此測試專案中的測試，您團隊上的其他成員將必須使用自己的認證，來重新設定測試專案。 若要這樣做，他們會編輯他們自己的 app.config 檔案複本，或是使用專案組態對話方塊。  
  
## <a name="permissions"></a>權限  
測試指令碼會在執行內容權限等級執行，也就是在一般使用情況下，於資料庫執行的使用者命令有效的相同權限等級。 測試前動作、測試後動作、TestInitialize 和 TestCleanup 指令碼都會在授權的內容權限等級執行。  
  
由於用於測試後動作指令碼之較高權限連接的緣故，所以您可以在其中執行驗證。 在此指令碼中，您也可以執行指令碼命令來測試權限。 如需有關權限的詳細資訊，請參閱 [SQL Server Data Tools 的必要權限](../ssdt/required-permissions-for-sql-server-data-tools.md)的 SQL Server 單元測試一節。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 單元測試中的指令碼](../ssdt/scripts-in-sql-server-unit-tests.md)  
[SQL Server 單元測試檔案](../ssdt/sql-server-unit-test-files.md)  
  
