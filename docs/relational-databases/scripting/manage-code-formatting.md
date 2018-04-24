---
title: 管理程式碼格式設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- indenting code [SQL Server]
- displaying URLs
- code formatting [SQL Server Management Studio]
- collapsing text
- formats [SQL Server], code formatting in SQL Server Management Studio
- hiding text
- formats [SQL Server]
- text [SQL Server], code formats
- automatic indentation
- converting text to lower case
- Query Editor [SQL Server Management Studio], managing code formats
- URL displayed in code [SQL Server Management Studio]
- converting text to upper case
- text [SQL Server]
- unindenting code
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 39aa0603bd5932c9b36185abacc56cc01e2aff19
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="manage-code-formatting"></a>管理程式碼格式設定
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  當使用編輯器時，您可以利用縮排、隱藏文字、URL...等，來建立程式碼的格式。 您也可以利用智慧型縮排 (Smart Indenting) 功能，在輸入程式碼的同時，自動建立程式碼的格式。  
  
## <a name="indenting"></a>縮排  
 您可以選擇三種不同的文字縮排樣式。 您也可以指定幾個空格組成單一縮排和定位點，以及編輯器在縮排時要使用定位字元或空格字元。  
  
#### <a name="to-choose-an-indenting-style"></a>選擇縮排樣式  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  按一下 **[文字編輯器]**。  
  
3.  按一下資料夾，選取 [所有語言] 來設定所有語言的縮排。  
  
4.  按一下 [定位點]。  
  
5.  請按一下下列其中一個選項：  
  
    -   **None**： 游標會移至下一行的開頭。  
  
    -   [區塊]。 游標會對齊上下行。  
  
    -   [智慧型] (預設)。 語言服務會決定要使用的適當縮排樣式。  
  
    > [!NOTE]  
    >  有些語言並未完整提供這三個縮排選項。  
  
#### <a name="to-change-indent-tab-settings"></a>變更縮排程位點設定  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  按一下 **[文字編輯器]**。  
  
3.  選取 [所有語言] 的資料夾來設定所有語言的縮排。  
  
4.  按一下 [定位點]。  
  
5.  若要指定縮排和定位作業的定位字元，請按一下 [保留定位點]。 若要指定空格字元，請選取 [插入空格]。  
  
     如果您選取 [插入空格]，請在 [定位點大小] 或 [縮排大小] 之下，分別輸入每個定位點或縮排所代表的空格字元數。  
  
#### <a name="to-indent-code"></a>縮排程式碼  
  
1.  選取您要縮排的文字。  
  
2.  按 TAB 鍵，或按一下 [標準] 工具列上的 [縮排] 按鈕。  
  
#### <a name="to-unindent-code"></a>取消縮排程式碼  
  
1.  選取您要取消縮排的文字。  
  
2.  按 SHIFT+TAB 鍵，或按一下 [標準] 工具列上的 [取消縮排] 按鈕。  
  
#### <a name="to-automatically-indent-all-of-your-code"></a>自動縮排所有程式碼  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  按一下 **[文字編輯器]**。  
  
3.  按一下 **[所有語言]**。  
  
4.  按一下 [定位點]。  
  
5.  按一下 [智慧型]。  
  
> [!NOTE]  
>  有些語言無法使用 [智慧型] 選項。  
  
#### <a name="to-convert-white-space-to-tabs"></a>將空格轉換成定位點  
  
1.  選取空格要轉換成定位點的文字。  
  
2.  在 [編輯] 功能表上，指向 [進階]，再按一下 [將選取範圍空白鍵轉定點]。  
  
#### <a name="to-convert-tabs-to-spaces"></a>將定位點轉換成空格  
  
1.  選取您要將定位點轉換成空格的文字。  
  
2.  在 [編輯] 功能表上，指向 [進階]，再按一下 [將選取範圍定位點轉空白]。  
  
 這些命令的行為會隨著 [選項] 對話方塊中的定位點設定而不同。 例如，如果定位點設定是 4，[將選取範圍空白鍵轉定點] 會每 4 個連續空格建立一個定位點，[選取範圍定位鍵轉空白鍵] 會每個定位點建立 4 個空格。  
  
## <a name="converting-text-to-upper-and-lower-case"></a>將文字轉換成大寫和小寫  
 您可以利用命令，將文字轉換成全為大寫或小寫。  
  
#### <a name="to-switch-text-to-upper-or-lower-case"></a>將文字切換成大寫或小寫  
  
1.  選取您要轉換的文字。  
  
2.  若要將文字轉換成大寫，請按 CTRL+SHIFT+U，或按一下 [編輯] 功能表 [進階] 子功能表中的 [設成大寫]。  
  
3.  若要將文字轉換成小寫，請按 CTRL+SHIFT+L，或按一下 [編輯] 功能表 [進階] 子功能表中的 [設成小寫]。  
  
> [!NOTE]  
>  如需完整的鍵盤快速鍵清單，請參閱[SQL Server Management Studio 鍵盤快速鍵](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)。  
  
## <a name="displaying-and-linking-to-urls"></a>顯示和連結到 URL  
 您可以在程式碼中，建立和顯示可點按的 URL。 依預設，這些 URL：  
  
-   會附加底線。  
  
-   當滑鼠指標移到這些 URL 上時，滑鼠指標會變成手的形狀。  
  
-   如果 URL 有效，當按一下 URL 時，會打開它。  
  
#### <a name="to-display-a-clickable-url"></a>顯示可點按的 URL  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  按一下 **[文字編輯器]**。  
  
3.  若要變更單一語言的選項，請按一下這個語言資料夾，再按一下 [一般]。 若要變更所有語言的選項，請按一下 [所有語言]，再按一下 [一般]。  
  
4.  選取 [啟用按一下方式的 URL 導覽]。  
  
  
