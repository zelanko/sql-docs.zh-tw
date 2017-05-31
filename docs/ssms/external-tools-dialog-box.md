---
title: "外部工具對話方塊 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding external tools
- external tools [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], external tools
ms.assetid: ba797203-24d0-4922-9b97-8ab483f1db14
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 96e4b3799c478e219308a121bb31713ac171ddcb
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="external-tools-dialog-box"></a>外部工具對話方塊
請利用 [外部工具] 對話方塊，將 SQLCMD 或 [記事本] 之類的外部工具新增至 [工具] 功能表。 新增外部工具可讓您在 [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 環境中工作時，輕易地啟動其他應用程式。 啟動工具時，您可以指定引數和工作目錄。 此外，某些工具的輸出可以顯示在 [輸出] 視窗中。 [外部工具] 對話方塊可以透過 [工具] 功能表使用。  
  
## <a name="options"></a>選項。  
**功能表內容**  
列出目前已新增至 [工具] 功能表之項目的標題。 使用 [上移] 與 [下移] 箭頭，可變更功能表上所示項目的順序。 使用 [刪除] 按鈕可從功能表中移除項目。  
  
**上移**  
在 [工具] 功能表所顯示的工具清單中，將所選的工具向上移動至較前面的位置。  
  
**下移**  
在 [工具] 功能表所顯示的工具清單中，將所選的工具向下移動至較後面的位置。  
  
**[加入]**  
清除文字方塊，讓您指定新的工具。  
  
**Delete**  
從 [功能表內容] 清單及 [工具] 功能表中移除工具或命令。  
  
**Title**  
輸入會顯示在 [工具] 功能表之 [外部工具] 子功能表上的工具名稱或命令。 將連字號 (&) 放在工具名稱的某個字母前，以指定該字母做為鍵盤快速鍵。 例如，"&SQLCMD" 會在 [工具] 功能表中顯示 SQLCMD。  
  
**Command**  
指定要啟動的檔案路徑。  
  
**引數**  
在功能表上選取工具時，指定會傳遞至該工具的變數。 啟動工具或命令時，引數可以指定會傳遞至該工具或命令的值。 例如，值可以指定檔案名稱或目錄。 請利用箭頭按鈕，從預先定義的引數清單中選取。 您可以加入一個以上。 如需預先定義的引數及其定義的完整清單，請參閱 [外部工具的引數](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)。 您也可以視所使用的命令或工具來輸入自訂引數 (例如，命令列參數)。  
  
**使用輸出視窗**  
開啟 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 的 [輸出] 視窗以顯示執行命令的輸出。 並非所有的工具都能以 [輸出] 視窗中所顯示的格式來輸出。 如需詳細資訊，請參閱 [輸出視窗](http://msdn.microsoft.com/en-us/9808e00c-c8f6-45cc-896e-192b8420f747)。  
  
**將輸出視為 Unicode**  
將輸出解譯為 Unicode。  
  
**初始目錄**  
指定工具的工作目錄。 請利用箭頭按鈕來選取目錄。 您可以選取一個以上。  
  
**提示提供引數**  
顯示 [引數] 對話方塊，讓您在每次啟動外部工具時，輸入或編輯引數的值。  
  
**結束時關閉**  
關閉工具時也關閉該工具所開啟的視窗。  
  
## <a name="example"></a>範例  
在 [外部工具] 對話方塊中輸入下列值，將會建立標示為 DAC 的功能表項目；在選取該功能表項目時，會開啟命令提示字元，並使用專用管理員連接執行 **sqlcmd** 公用程式。  
  
|方塊|Value|  
|-------|---------|  
|**Title**|DAC|  
|**Command**|[!INCLUDE[ssInstallPath](../includes/ssinstallpath_md.md)]Tools\Binn\SQLCMD.exe|  
|**引數**|-A|  
  
## <a name="see-also"></a>另請參閱  
[外部工具的引數](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)  
[一般使用者介面元素](../ssms/general-user-interface-elements.md)  
  

