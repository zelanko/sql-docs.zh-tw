---
title: 使用方式和診斷資料
ms.custom: seo-lt-2019
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5b61b32ab266c4068f610b9138bf3fc8ea364f0e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245695"
---
# <a name="local-audit-for-ssms-usage-and-diagnostic-data-collection"></a>SSMS 使用方式和診斷資料收集的本機稽核
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server Management Studio (SSMS) 包含使用已連線到網際網路的功能，可收集匿名的功能使用方式和診斷資料並傳送給 Microsoft。 SSMS 可能會收集標準的電腦資訊以及關於使用方式和效能的資訊，這些資訊可能會傳送給 Microsoft，並基於改善 SSMS 的品質、安全性和可靠性的目的加以分析。 我們不會收集您的姓名、地址或是其他連絡資訊等資料。 如需詳細資訊，請參閱 [Microsoft 隱私權聲明](https://privacy.microsoft.com/privacystatement)和 [SQL Server 隱私權補充](https://go.microsoft.com/fwlink/?LinkID=868444)。

## <a name="audit-feature-usage-and-diagnostic-data"></a>稽核功能使用狀況和診斷資料

若要查看 SSMS 所收集的功能使用狀況資料，請執行下列步驟：

1.  啟動 SSMS。
2.  按一下 [檢視]  ，然後按一下主功能表中的 [輸出]  以顯示 [輸出]  視窗。 
3.  當 [輸出]  視窗顯示時，選擇 [顯示輸出來源:]  功能表中的 [遙測]  。

當您使用 SSMS 來與資料庫互動時，[輸出]  視窗會顯示所收集的資料。

## <a name="enable-or-disable-usage-and-diagnostic-data-collection-in-ssms"></a>啟用或停用 SSMS 中的使用狀況和診斷資料收集

選擇加入或選擇退出 SSMS 的使用方式資料收集：

- 針對 SQL Server Management Studio 17：

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\14.0`

  RegEntry name = `UserFeedbackOptIn`

  項目類型 `DWORD`:`0` 為退出；`1` 為選擇加入

  此外，SSMS 17.x 是以 Visual Studio 2015 Shell 為基礎，而 Visual Studio 安裝預設會啟用客戶回函。  

  若要在個別電腦上設定 Visual Studio 以停用客戶意見反應，請將下列登錄子機碼值變更為字串 `0`：`HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn`

  例如，將此子機碼變更如下：  
  `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn `=` 0`

  SQL Server 2017 使用方式和診斷資料收集會接受這些登錄子機碼上以登錄為基礎的群組原則。

- 針對 SQL Server Management Studio 18：

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\18.0_IsoShell`

  RegEntry name = `UserFeedbackOptIn`

  項目類型 `DWORD`:`0` 為退出；`1` 為選擇加入

## <a name="see-also"></a>另請參閱

- [設定 SQL Server 的使用狀況和診斷資料收集](../sql-server/usage-and-diagnostic-data-configuration-for-sql-server.md)
- [SQL Server 使用狀況和診斷資料收集的本機稽核](https://msdn.microsoft.com/library/mt743085.aspx)