---
description: 使用物件總管管理物件
title: 使用物件總管管理物件
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.SWB.SQLSERVEROBJECTEXPLORER.DHELP
helpviewer_keywords:
- Object Explorer F1 Help
- OE F1 Help
- OE Help
ms.assetid: e60367a7-3fdd-40b8-82bb-9e819d78de5a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 974cf89ca255f42f088d9b271863c45f4294fbbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491891"
---
# <a name="manage-objects-by-using-object-explorer"></a>使用物件總管管理物件
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以使用物件總管管理像是資料庫、資料表和預存程序等物件。  
  
## <a name="viewing-objects-in-object-explorer"></a>在物件總管中檢視物件  
物件總管會利用樹狀結構，將資訊分組成資料夾。 若要展開資料夾，請按一下加號 (+)，或按兩下資料夾。 展開資料夾來顯示更詳細的資訊。 以滑鼠右鍵按一下資料夾或物件來執行一般工作。 請按兩下物件來執行最平常的工作。  
  
您第一次展開資料夾時，物件總管會查詢伺服器來找出擴展樹狀結構的資訊。 當擴展樹狀結構時，您可以執行其他功能。 當物件總管在擴展樹狀結構時，您可以按一下 [停止]**** 來中止這個程序。 進一步的動作 (如篩選清單) 只會作用於資料夾擴展的部分，除非您重新整理資料夾來重新開始擴展。  
  
為了在有許多物件時能夠節省資源，[物件總管] 樹狀結構中的資料夾不會自動重新整理他們的內容清單。 若要重新整理資料夾內的物件清單，請以滑鼠右鍵按一下資料夾，再按一下 [重新整理]****。  
  
[物件總管] 只能顯示最多 65,536 個物件。 超出 65,536 個現有的物件之後，您便無法在 [物件總管] 樹狀檢視中，捲動瀏覽其他物件。 在 [物件總管] 中檢視其他物件，請關閉未使用的節點，或套用篩選來減少物件數目。  
  
## <a name="filtering-the-list-of-objects-in-object-explorer"></a>在 [物件總管] 中篩選物件清單  
當資料夾包含大量物件時，可能很不容易找到您要找的物件。 在這種情況下，請利用 [物件總管] 的篩選功能來縮減清單大小。 例如，您可能會想在包含數百個物件的清單中，尋找特定資料庫使用者或最近建立的資料表。 請按一下您要篩選的資料夾，再按一下篩選按鈕來開啟 [篩選設定]**** 對話方塊。 您可以依名稱、建立日期來篩選清單，有時也可以利用結構描述來篩選，且可以提供 [開頭為]****、[包含]**** 和 [介於]**** 之類的其他篩選運算子。  
  
## <a name="multi-select"></a>複選  
在 [物件總管] 中，每次只能選取一個物件。 若要選取多個項目，請按 **F7** 開啟 [物件總管詳細資料]**** 頁面。 [物件總管詳細資料]**** 頁面支援多重選取。  
  
## <a name="register-a-server-from-object-explorer"></a>從物件總管註冊伺服器  
當連接到伺服器時，您便很容易註冊伺服器，供未來使用。 在物件總管中，以滑鼠右鍵按一下伺服器名稱，然後按一下 [註冊]****。 在 [已註冊的伺服器]**** 對話方塊中，指定伺服器在伺服器群組樹狀結構中的放置位置。 在 [伺服器名稱]**** 方塊中，您可以將伺服器名稱改成更有意義的伺服器名稱。 例如，您可以利用類似 " **Accounts Payable** " 等更有意義的名稱來註冊**APSQL02**伺服器。  
  
## <a name="performing-actions-on-object-explorer-nodes"></a>在物件總管節點上執行動作  
以滑鼠右鍵按一下表示物件的物件總管節點，針對物件執行動作。 每種物件類型都支援一組唯一的按右鍵動作。 您可以使用按右鍵功能表執行的某些動作類型包括：  
  
### <a name="open-a-connected-query-editor"></a>開啟連接的查詢編輯器  
當物件總管連接到伺服器時，您可以利用 [物件總管] 的連接設定來開啟新的 [程式碼編輯器] 視窗。 若要開啟新的 [程式碼編輯器] 視窗，請在物件總管中，以滑鼠右鍵按一下伺服器名稱，再按一下 [新增查詢]****。 若要利用特定資料庫來開啟 [程式碼編輯器] 視窗，請以滑鼠右鍵按一下資料庫名稱，再按一下 [新增查詢]****。 當開啟 Analysis Services 伺服器的新查詢時，您可以選取 DMX、MDX 或 XMLA 查詢。  
  
### <a name="start-powershell"></a>啟動 PowerShell  
您可以啟動 PowerShell 工作階段，其方式是以滑鼠右鍵按一下物件總管樹狀結構中的大多數資料夾和物件，然後選取 [啟動 PowerShell]。 這樣會啟動 PowerShell 工作階段，此工作階段已啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 支援，而且路徑會設定為您在 [物件總管] 中以滑鼠右鍵按一下的物件。 然後您可以在互動式 PowerShell 環境中輸入 PowerShell 命令。 如需詳細資訊，請參閱 [SQL Server PowerShell](https://msdn.microsoft.com/89b70725-bbe7-4ffe-a27d-2a40005a97e7)。  
  
## <a name="see-also"></a>另請參閱  
[物件總管](../../ssms/object/object-explorer.md)  
[開啟和設定物件總管](../../ssms/object/open-and-configure-object-explorer.md)  
[從物件總管連接到執行個體](../../ssms/object/connect-to-an-instance-from-object-explorer.md)  
[物件總管詳細資料窗格](../../ssms/object/object-explorer-details-pane.md)  
[Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)  
  
