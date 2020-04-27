---
title: 提供 SQL Server 2014 的意見反應 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sending feedback to Microsoft
- errors [SQL Server], feedback reporting
- feedback [SQL Server]
- submitting feedback [SQL Server]
- bug reporting [SQL Server]
- reporting usage information to Microsoft
- reporting errors to Microsoft
- SQL Server, feedback reporting
- documentation feedback [SQL Server]
- usage information reporting [SQL Server]
- product feedback [SQL Server]
- automatic error or usage reporting
ms.assetid: 28f3ebf0-ad71-4816-86a6-18a46f023cfe
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10466721f50dd8b090b5d6b1a06b5bffd6e5289d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62772274"
---
# <a name="providing-feedback-for-sql-server-2014"></a>提供關於 SQL Server 2014 的回函
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 感謝您撥冗協助我們改良 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 產品和文件集。 您可以提供有關產品功能和使用者介面的建議與錯誤報告、提交文件集回函，以及選擇將錯誤報告和使用方式資料自動傳送給 [!INCLUDE[msCoName](../includes/msconame-md.md)] 進行分析。 這三個回函選項分述如下。  
  
## <a name="submitting-feedback-about-the-product"></a>提交關於產品的回函  
 您可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Connect 上的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 回函頁面，傳送關於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能的建議和錯誤報告。 這些功能可包括工具與公用程式、語言以及程式設計介面等。  
  
 您可以利用許多方式尋找 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 回函頁面。  
  
-   移至 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 回函[網頁](https://go.microsoft.com/fwlink/?linkid=34178)。  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的說明工具列上按一下 [傳送回函]**** 按鈕，或選取 [社群/傳送回函]**** 命令。  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的說明工具列上，按一下 [傳送回函]**** 按鈕。  
  
-   在《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》的任何主題頂端，按一下 [傳送回函]**** 按鈕。  
  
 在您執行下列任一動作前，說明工具列不會顯示在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中：  
  
-   從公用程式存取說明。  
  
-   在 [**工具]/[自訂 ...** ] 命令的 [**工具列**] 索引標籤上，選取 [說明 **] 核取方塊**。  
  
## <a name="automatic-error-and-usage-reporting"></a>自動錯誤和使用方式報告  
 您可以啟用自動報告錯誤及傳送有關如何使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 軟體和服務之資料的功能。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 會利用這些資訊來改善 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 並將所有資料視為機密。  
  
### <a name="managing-automatic-usage-reporting"></a>管理自動使用方式報告  
 自動使用方式報告可讓您決定是否要收集及傳送資料給 [!INCLUDE[msCoName](../includes/msconame-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會使用兩種管線來報告使用方式資料。 這兩個管線會報告類似的資料，不過分別報告不同程式的資料，而且可以單獨開啟或關閉。 使用任何一個程式來開啟或關閉管線時，也會使其他共用相同管線的程式停止或啟動資料收集。  
  
-   除了線上叢書和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具中某些 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 使用者介面元素外，我們使用單一管線來報告所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的使用方式資料。 在安裝之後，您也可以關閉 (或開啟) 此管線。 若要這樣做，請在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 專案，然後從 [說明]**** 功能表中選取 [客戶回函選項]****。 除非您已開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 專案，否則這個命令不會出現。  
  
-   其他管線會用於《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具的 Visual Studio 使用者介面及 Visual Studio。 在安裝之後，您也可以關閉 (或開啟) 此管線。 若要這樣做，請在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 專案，然後從 [說明]**** 功能表中選取 [客戶回函選項]****。 除非您已開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 專案，否則這個命令不會出現。  
  
## <a name="helping-build-a-better-books-online"></a>協助建立更完善的線上叢書  
 藉由選擇啟用《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》的使用方式報告，將可協助小組開發更完善的文件集。 我們收到的彙總資料將可幫助我們了解客戶的需要。 我們會了解客戶如何在主題之間移動、客戶檢視特定主題的頻率，以及客戶認為哪些主題最有用處及最沒用處。  
  
 您的回函可讓我們了解您如何使用文件集。 這有助於將我們的撰寫資源配置給最重要的主題，並針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 設計未來的文件集系統。 線上叢書中的使用資訊也可幫助我們識別客戶經常針對哪些功能搜尋說明。 這樣可為我們指示可能需要改進可用性的地方。  
  
  
