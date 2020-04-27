---
title: 外部工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 264eb3c9b16c5eb12a578090d55e4f64884177c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62649689"
---
# <a name="external-tools"></a>外部工具
  使用此對話方塊可將外部工具 (例如 SQL Server 組態管理員或記事本) 新增到 [工具]  功能表。 加入外部工具可以讓您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中工作時，輕易地啟動其他應用程式。 啟動工具時，您可以指定引數和工作目錄。 除此之外，某些工具的輸出也可以顯示在 [輸出] 視窗中。 [外部工具]  對話方塊可以透過 [工具]  功能表使用。  
  
## <a name="options"></a>選項。  
 **功能表內容**  
 列出目前已新增至 [工具]  功能表之項目的標題。 使用 [上移]  與 [下移]  箭頭，可變更功能表上所示項目的順序。 使用 [刪除]  按鈕可從功能表中移除項目。  
  
 **上移**  
 在 [工具]  功能表所顯示的工具清單中，將所選的工具向上移動至較前面的位置。  
  
 **下移**  
 在 [工具]  功能表所顯示的工具清單中，將所選的工具向下移動至較後面的位置。  
  
 **加入**  
 清除文字方塊，讓您指定新的工具。  
  
 **刪除**  
 從 [功能表內容]  清單及 [工具]  功能表中移除工具或命令。  
  
 **Title** (標題)  
 出現在 [工具]  功能表之 [外部工具]  子功能表上的工具名稱或命令名稱。 將連字號 (&) 放在工具名稱中的字母前，即可使用該字母作為工具的加速鍵。 例如 `&Spy++` 在 [工具]  功能表上會顯示為 **Spy++** 。  
  
 **命令**  
 指定 .exe、.com、.pif、.bat、.cmd，或其他您想要啟動之檔案的路徑。 若選取 [使用輸出視窗]`.bat``.com` 核取方塊，即可在輸出視窗中檢視  及其他檔案的輸出。  
  
 **引數**  
 在功能表上選取工具時，指定會傳遞至該工具的變數。 啟動工具或命令時，引數可以指定會傳遞至該工具或命令的值。 例如，值可以指定檔案名稱或目錄。 使用 **箭號** 按鈕，可從預先定義的引數清單中選取引數。 您可以加入一個以上。 如需預先定義的引數及其定義的完整清單，請參閱 [外部工具的引數](external-tools.md)。 視您所使用的命令或工具而定，還可以輸入自訂引數 (例如，命令提示字元參數)。  
  
 **初始目錄**  
 指定工具的工作目錄。 使用 **箭號** 按鈕可選取目錄。 您可以選取一個以上。  
  
 **使用輸出視窗**  
 指定工具的結果是否要顯示在 [輸出] 視窗中。 此選項僅適用於通常會在命令提示視窗中顯示輸出的檔案 (例如 .bat 和 .com 檔案)。 若啟用此選項，當您要追蹤工具的進度時，此選項可以簡化視窗的管理。  
  
 **提示提供引數**  
 顯示 [引數]  對話方塊，讓您每次啟動外部工具時，都能輸入或編輯引數的值。  
  
 **將輸出視為 Unicode**  
 允許 [輸出] 視窗接受 Unicode。  
  
 **結束時關閉**  
 關閉工具時也關閉該工具所開啟的視窗。  
  
## <a name="example"></a>範例  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>將 SQL Server 組態管理員新增到工具功能表  
  
1.  在 [工具]  功能表上按一下 [外部工具]  。  
  
2.  在 [標題]  方塊中，輸入 SQL Server 組態管理員  。  
  
3.  在 [**命令**] 方塊中，輸入[!INCLUDE[msCoName](../../includes/msconame-md.md)]管理主控台可執行檔的路徑，例如`C:\WINNT\system32\mmc.exe`  
  
4.  在 [**引數**] 方塊中，輸入 .msc 檔案的路徑，例如`"C:\WINNT\system32\SQLServerManager.msc"`  
  
> [!NOTE]  
>  檢視 [開始][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**功能表上之**  捷徑的屬性，以確認這些檔案在您電腦上的位置。  
