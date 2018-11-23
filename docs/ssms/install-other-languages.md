---
title: 安裝非英文語言版本的 SQL Server Management Studio (SSMS) | Microsoft Docs
description: 安裝非英文語言版本的 SQL Server Management Studio (SSMS)
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a33053220184dfc58b0e0f6ccfb9526b5cb3ea5
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51697116"
---
# <a name="install-non-english-language-versions-of-sql-server-management-studio-ssms"></a>安裝非英文語言版本的 SQL Server Management Studio (SSMS) 

[SSMS 提供數種語言版本](download-sql-server-management-studio-ssms.md#available-languages-ssms-179)，但是當系統地區設定與 SSMS 語言不相符時，SSMS 安裝程式會封鎖電腦上的安裝。 

下列指示會依您的 Windows 版本而有所不同。 下列指示適用於 Windows 10。

## <a name="install-non-english-ssms-on-a-computer-running-an-english-operating-system-os"></a>在執行英文版作業系統 (OS) 的電腦上安裝非英文版 SSMS

1. 針對您希望 SSMS 所使用的語言，安裝此語言的 Windows 語言套件： 
   - [設定] > [時間與語言] > [區域與語言] > [新增語言] 
2. 現在按一下剛剛安裝的語言，然後選取 [設為預設值]，以便將系統地區設定設為使用先前步驟中所安裝的語言套件。 (安裝 SSMS 之後，您可以將系統地區設定重新設定為英文)。
3. 當作業系統以您所要的語言執行之後，[SSMS 會提供述種語言版本](download-sql-server-management-studio-ssms.md#available-languages-ssms-179)。 第一次安裝新的 SSMS 語言時，請使用完整的套件。 針對後續安裝，您可以使用升級套件。
4. 執行 SSMS，它應該會以您在先前步驟中所安裝的語言來顯示。
5. 將電腦的系統地區設定重新設定為英文。

## <a name="install-ssms-in-a-language-other-than-the-language-of-the-installed-os"></a>以不同於所安裝作業系統語言版本的語言來安裝 SSMS

1. 針對您希望 SSMS 所使用的語言，安裝此語言的 Windows 語言套件： 
   - [設定] > [時間與語言] > [區域與語言] > [新增語言] 
2. 現在按一下剛剛安裝的語言，然後選取 [設為預設值]，以便將系統地區設定設為使用先前步驟中所安裝的語言套件。 
3. 當作業系統以您所要的語言執行之後，[SSMS 會提供述種語言版本](download-sql-server-management-studio-ssms.md#available-languages-ssms-179)。 第一次安裝新的 SSMS 語言時，請使用完整的套件。 針對後續安裝，您可以使用升級套件。
4. 針對您想要安裝但不符合已安裝初版 SSMS 語言的每種語言，請安裝對應的 Visual Studio 2015 Shell (獨立模式) 語言套件：
   - 瀏覽至 [https://connect.microsoft.com/VisualStudio/ExtendVS](https://connect.microsoft.com/VisualStudio/ExtendVS) (您可能需要登入並完成「連線註冊」程序)。
   - 下載所需的 Visual Studio 2015 Shell (獨立模式) 語言套件並加以安裝。

   > [!IMPORTANT]
   > 請使用先前的步驟來安裝 Visual Studio 2015 Shell (獨立模式) 語言套件，不要使用 [工具] | [選項] | [國際設定] 上的 [取得其他語言] 連結。 

5. 執行 SSMS，並選取您想要使用的語言：
   - [工具] | [選項] | [國際設定]
1. 關閉並重新啟動 SSMS。

## <a name="next-steps"></a>後續步驟

- [教學課程：SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/tutorial-sql-server-management-studio)
