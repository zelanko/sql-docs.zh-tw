---
title: 管理編輯器和檢視模式 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], managing window behavior
- workbench view modes [SQL Server Management Studio]
- full screen mode [SQL Server Management Studio]
- fonts [SQL Server Management Studio]
- word wraps [SQL Server Management Studio]
- virtual space mode [SQL Server Management Studio]
- splitting document views
- displaying line numbers
- view modes [SQL Server Management Studio]
ms.assetid: 25c58a14-9f94-4296-9770-7d84c6bc3969
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a141abd42c1a3d8c15dc2b96b1637ea2775072f
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67680205"
---
# <a name="manage-the-editor-and-view-mode"></a>管理編輯器和檢視模式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  編輯器提供了許多用來控制程式碼檢視的方式。  
  
## <a name="changing-the-view-mode"></a>變更檢視模式  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 有一個稱為 **[索引標籤文件]** 的檢視模式，您可以利用這個模式來同時開啟多個編輯器和多份文件，並利用編輯器頂端的索引標籤來存取它們。 另外，您也可以在多重文件介面 (MDI) 模式中開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 環境，此時會將不含索引標籤的各個視窗聯結起來，您可以並排這些視窗、將它們最小化...等等。  
  
#### <a name="to-switch-between-view-modes"></a>切換檢視模式  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  按一下 **[環境]** 。 按一下 **[一般]** 。  
  
3.  按一下 **[索引標籤文件]** 或 **[MDI 環境]** 。  
  
    > [!NOTE]  
    >  您必須重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，變更才會生效。  
  
## <a name="splitting-the-view"></a>分割檢視  
 您可以將 [編輯器] 視窗分割成兩個部份，使編輯工作更容易進行。  
  
#### <a name="to-split-a-window"></a>分割視窗  
  
1.  按一下分割線 (在捲軸上面)。  
  
2.  向下拖曳分割線。  
  
3.  若要返回單一窗格，請按兩下用來分隔兩個窗格的分割線。  
  
 新的窗格包含相同的文件，只要窗格是顯示文件中的相同位置，一個窗格中的變更，也會反映在另一個窗格中。  
  
## <a name="word-wrap"></a>自動換行  
 當您啟動自動換行時，會移除水平捲軸，您不需要捲動視窗，超出編輯器視窗寬度的各行程式碼會自動折行。  
  
#### <a name="to-activate-word-wrap"></a>啟動自動換行  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  按一下 **[文字編輯器]** 。  
  
3.  開啟適當語言資料夾 (或 [所有語言]  ，這會影響所有語言)。  
  
4.  選取 **[自動換行]** 。  
  
## <a name="enabling-virtual-space-mode"></a>啟用虛擬空間模式  
 在 **[虛擬空間]** 模式中，編輯器的行為會如同各行尾端之後的空間填滿了無數個空格，可讓各行程式碼延伸到超出可見螢幕區的側邊。  
  
#### <a name="to-enable-virtual-space-mode"></a>啟用虛擬空間模式  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  按一下 **[文字編輯器]** 。  
  
3.  開啟適當語言資料夾 (或 [所有語言]  ，這會影響所有語言)。  
  
4.  選取 **[啟用虛擬空間]** 。  
  
 當啟用虛擬空間模式時，游標會從行尾折返到下一行的第一個字元，反之亦然。  
  
## <a name="displaying-line-numbers"></a>顯示行號  
 您可以在程式碼中開啟顯示行號的功能。 在導覽程式碼時，行號非常有用。 如需詳細資訊，請參閱 [導覽程式碼與文字](../../relational-databases/scripting/navigate-code-and-text.md)。  
  
> [!NOTE]  
>  開啟顯示行號的功能，不表示列印文件時會有行號。 若要列印行號，您必須在 **[檔案]** 功能表的 **[版面設定]** 命令中，選取 **[行號]** 核取方塊。  
  
#### <a name="to-display-line-numbers-in-code"></a>在程式碼中顯示行號  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  按一下 **[文字編輯器]** 。  
  
3.  按一下 **[所有語言]** 。  
  
4.  按一下 **[一般]** 。  
  
5.  選取 **[行號]** 。  
  
 如果只要針對某些程式設計語言指定顯示行號的功能，請在適當資料夾中選取 **[行號]** 。  
  
## <a name="enabling-full-screen-mode"></a>啟用全螢幕模式  
 您可以選擇隱藏所有工具視窗，啟用全螢幕模式來專門檢視文件視窗。  
  
#### <a name="to-enable-full-screen-mode"></a>啟用全螢幕模式  
  
1.  按 ALT+SHIFT+ENTER 來切換全螢幕模式。  
  
## <a name="using-auto-hide-all"></a>使用 [自動全部隱藏]  
  
#### <a name="to-hide-all-the-tool-windows-at-once"></a>同時隱藏所有工具視窗  
  
1.  在 **[視窗]** 功能表上，按一下 **[自動全部隱藏]** 。  
  
  
