---
title: 解除安裝單機版報表產生器 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 3fec5ecbe30bb55262a274b5764d6650044a54a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216848"
---
# <a name="uninstall-the-stand-alone-version-of-report-builder-report-builder"></a>解除安裝單機版報表產生器 (報表產生器)
  您可以從控制台或命令列解除安裝單機版本的報表產生器。 如果沒有解除安裝 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)]，您就不能解除安裝 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 版本的報表產生器。  
  
 從命令列解除安裝報表產生器所用的語法與用來安裝報表產生器的語法完全相同，不過您會使用 /x 選項來取代 /i 選項。 解除安裝的命令列也可以包含 /quiet 選項和其他標準選項。 如果已經移除了報表產生器的 Windows Installer 套件 (ReportBuilder3_x86.msi)，您就無法輕鬆地使用命令列來解除安裝報表產生器。 若要深入了解有關如何使用 GUID 來移除報表產生器的詳細資訊，請參閱 MSDN Library 上 msiexec 程式的文件集。  
  
 如果報表產生器使用的資料夾包含自訂檔案，移除報表產生器時便會保留這些資料夾和檔案。 系統只會移除報表產生器的檔案。  
  
### <a name="to-uninstall-report-builder-from-the-control-panel"></a>若要從控制台解除安裝報表產生器  
  
1.  在 **[開始]** 功能表上，按一下 **[控制台]**。  
  
2.  在 [控制台] 中，按一下 **[程式和功能]**。  
  
3.  在 [名稱] 清單中找出 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表產生器，然後按一下它。  
  
4.  按一下 **[解除安裝]**。  
  
5.  如果出現確認解除安裝報表產生器的提示，請按一下 **[是]**。  
  
### <a name="to-uninstall-report-builder-from-the-command-line"></a>若要從命令列解除安裝報表產生器  
  
1.  在 **[開始]** 功能表上，按一下 **[執行]**。  
  
2.  在 **開啟**文字方塊中，輸入 `cmd.`  
  
3.  在 [命令提示字元] 視窗中，導覽至包含 ReportBuilder3_x86.msi 的資料夾。  
  
4.  輸入如下的基本命令列：  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 如果可以包含記錄功能，請使用如下所示的命令列：  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
1.  按 **Enter**鍵。  
  
## <a name="see-also"></a>另請參閱  
 [安裝、 解除安裝與報表產生器支援](../install-uninstall-and-report-builder-support.md)   
 [安裝單機版本報表產生器的&#40;報表產生器&#41;](install-report-builder.md)  
  
  
