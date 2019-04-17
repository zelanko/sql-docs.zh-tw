---
title: 設定 SQL Server 工具的使用方式和診斷資料收集 | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: baf3a205-a6bb-4564-8b64-3a0475bb9273
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c60eb8cac357fba523196385e72a1b05a2c36f4
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2019
ms.locfileid: "59243512"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-tools"></a>設定 SQL Server 工具的使用方式和診斷資料收集

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

了解客戶經驗改進計畫 (CEIP) 如何協助 Microsoft 找出可讓我們的軟體變得更好的方法。  您隨時都能設定工具來選擇加入或退出。  
  
> [!NOTE]  
> 如需 Microsoft SQL Server 版本的使用者資料收集與使用方式的說明，請參閱這份[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)。  
  
## <a name="opting-in-and-out-of-ceip-for-sql-server-data-tools"></a>選擇加入和退出 SQL Server Data Tools 的 CEIP  

 客戶經驗改進計畫是設計來協助 Microsoft 在經過一段時間之後改進其產品的計畫。 此計畫會收集電腦硬體相關資訊以及使用者如何使用我們的產品，而不會中斷使用者在電腦上的工作。 所收集的資訊可協助 Microsoft 找出應改善的功能。 在本文件中，我們將討論如何針對 Visual Studio 2017、Visual Studio 2015 和 Visual Studio 2013 選擇加入或退出 SQL Server Data Tools (SSDT) 的 CEIP。  

### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2017"></a>選擇與控制 CEIP 與 SQL Server Data Tools for Visual Studio 2017

 Visual Studio 2017 的 SSDT 是隨附於 SQL Server 2017 的資料模型化工具。 它會使用內建於 Visual Studio 2017 的 CEIP 選項。 您可以從這份 [Visual Studio 的說明文件](https://www.visualstudio.com/docs/work/connect/give-feedback)深入了解如何在 Visual Studio 2017 中透過 CEIP 提交意見反應。  
  
 如果是 SQL Server 2017 的預覽版本，預設會開啟 CEIP。 您可以依照下列指示來將它關閉或重新開啟。  
  
 **在 Visual Studio (適用於 Visual Studio 2017 的完整語言安裝) 中**  
  
 如果您在已經具備 Visual Studio 的電腦上執行 SSDT 安裝程式，就只會新增 SQL Server 和商業智慧專案範本。 在此案例中，Visual Studio 提供的客戶回函選項可用來選擇加入或退出 CEIP。  
  
1.  啟動 Visual Studio。  
  
2.  從 [說明] 功能表中，選取 [傳送意見反應]  >  [設定]。  
  
3.  若要關閉 CEIP，請按一下 [否，我不願意參加]，然後按一下 [確定]。  
  
     若要開啟 CEIP，請按一下 [是，我願意參加]，然後按一下 [確定]。  
  

  
 **使用以登錄為基礎的原則或群組原則**  
  
 如果您在沒有 Visual Studio 2017 的電腦上執行 SSDT 安裝程式，則只會安裝 Visual Studio Shell。 此命令介面並未提供客戶回函選項。 在此情況下，登錄更新是用來設定 CEIP 的唯一選項  
  
 企業客戶可以建構群組原則，藉由設定適用於 SQL Server 2017 之以登錄為基礎的原則，選擇加入或退出。  
  
 相關的登錄機碼與設定如下：  
  
- 64 位元作業系統，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\15.0\SQM
- 32 位元作業系統，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\15.0\SQM

啟用群組原則時，Key = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM 

Entry = OptIn

Value = (DWORD)
- 0 為選擇退出 (關閉 VSCEIP)
- 1 為選擇加入 (開啟 VSCEIP)

  
> [!CAUTION]  
>  不當編輯登錄可能會造成系統嚴重受損。 在變更登錄之前，應備份電腦上的所有重要資料。 如果　貴用戶在套用手動變更之後遇到問題，也可以使用 [上次的正確設定] 啟動選項。  
  
 如需 CEIP 所收集、處理或傳輸之資訊的詳細資訊，請參閱[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)。  
 
### <a name="choice-and-control-over-ceip-and-sql-server-data-tools-for-visual-studio-2015"></a>選擇和控制 CEIP 與 SQL Server Data Tools for Visual Studio 2015  
 Visual Studio 2015 的 SSDT 是隨附於 SQL Server 2016 的資料模型化工具。 它會使用內建於 Visual Studio 2015 的 CEIP 選項。 您可以從這份 [Visual Studio 的說明文件](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)深入了解如何在 Visual Studio 2015 中透過 CEIP 提交意見反應。  
  
 如果是 SQL Server 2016 的預覽版本，預設會開啟 CEIP。 您可以依照下列指示來將它關閉或重新開啟。  
  
 **在 Visual Studio (適用於 Visual Studio 2015 的完整語言安裝) 中**  
  
 如果您在已經具備 Visual Studio 的電腦上執行 SSDT 安裝程式，就只會新增 SQL Server 和商業智慧專案範本。 在此案例中，Visual Studio 提供的客戶回函選項可用來選擇加入或退出 CEIP。  
  
1.  啟動 Visual Studio。  
  
2.  從 [說明] 功能表中，選取 [傳送意見反應]  >  [設定]。  
  
3.  若要關閉 CEIP，請按一下 [否，我不願意參加]，然後按一下 [確定]。  
  
     若要開啟 CEIP，請按一下 [是，我願意參加]，然後按一下 [確定]。  
  

  
 **使用以登錄為基礎的原則或群組原則**  
  
 如果您在沒有 Visual Studio 2015 的電腦上執行 SSDT 安裝程式，則只會安裝 Visual Studio Shell。 此命令介面並未提供客戶回函選項。 在此情況下，登錄更新是用來設定 CEIP 的唯一選項  
  
 企業客戶可以建構群組原則，藉由設定適用於 SQL Server 2016 之以登錄為基礎的原則，選擇加入或退出。  
  
 相關的登錄機碼與設定如下：  
  
 機碼 = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\14.0\SQM  
  
 登錄項目名稱 = OptIn  
  
 項目類型 DWORD：  
  
-   0 為關閉  
  
-   1 為開啟  
  
> [!CAUTION]  
>  不當編輯登錄可能會造成系統嚴重受損。 在變更登錄之前，應備份電腦上的所有重要資料。 如果　貴用戶在套用手動變更之後遇到問題，也可以使用 [上次的正確設定] 啟動選項。  
  
 如需 CEIP 所收集、處理或傳輸之資訊的詳細資訊，請參閱[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)。  
  
### <a name="choice-and-control-for-ceip-and-sql-server-data-tools---bi-ssdt-bi"></a>選擇與控制 CEIP 與 SQL Server Data Tools - BI (SSDT-BI)  
 如果您正在使用 SSDT-BI，就有機會在安裝期間，選擇參加 CEIP。 稍後就能透過用戶端工具，或藉由編輯登錄設定來進行 SSDT-BI 的 CEIP 組態變更。  
  
 **在 SSDT 和適用於 Visual studio 2013 的 SSDT-BI 中**  
  
1.  啟動工具，並為 Analysis Services 或 Integration Services 中開啟新的或現有的專案。  
  
2.  從 [說明] 功能表中，選取 [Microsoft SQL Server 客戶回函選項] 。  
  
3.  若要關閉 CEIP，請按一下 [不，我不想參加] 。  
  
     若要開啟 CEIP，請按一下 [是，我願意參加] 。  
  
4.  按一下 [確定] 。  
  
 **使用以登錄為基礎的原則或群組原則**  
  
 企業客戶可以建構群組原則，藉由設定適用於 SQL Server 2014 之以登錄為基礎的原則，選擇加入或退出。  
  
 相關的登錄機碼與設定如下：  
  
 機碼 = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\120  
  
 登錄項目名稱 = CustomerFeedback  
  
 項目類型 DWORD：  
  
-   0 為關閉  
  
-   1 為開啟  
  
  
