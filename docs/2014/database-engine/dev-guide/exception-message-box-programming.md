---
title: 例外狀況訊息方塊程式設計 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- ExceptionMessageBox class, about ExceptionMessageBox class
- exception message box [SQL Server], about exception message box
- exception message box [SQL Server]
- interfaces [SQL Server]
- exceptions [SQL Server]
- messages [SQL Server], exception message box
ms.assetid: 0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b2425169f838199ce24b4331dd57c74b480adf62
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933621"
---
# <a name="exception-message-box-programming"></a>例外狀況訊息方塊程式設計
  例外狀況訊息方塊是以安裝的程式設計介面，並由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 圖形元件所使用。 例外狀況訊息方塊是支援的 Managed 組件，可讓您用於應用程式中，以便更有效地控制訊息經驗，以及讓使用者選擇要儲存錯誤訊息內容以供日後參考，或是取得訊息的相關說明。 由於所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都會安裝例外狀況訊息方塊 ([!INCLUDE[ssEW](../../includes/ssew-md.md)] 除外)，因此您可以在已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端元件的任何電腦上使用此功能，不需要進行其他組態設定。  
  
 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 命名空間中的 <xref:Microsoft.SqlServer.MessageBox> 類別具有 <xref:System.Windows.Forms.MessageBox> 類別的所有功能和其他功能。 <xref:System.Windows.Forms.MessageBox> 是為了適當地處理 Managed 程式碼例外狀況所設計的，所以適合使用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 的任何工作採用。 例外狀況訊息方塊可讓您執行下列作業：  
  
-   提供自訂的按鈕文字，最多五個按鈕。 按鈕和對話方塊的大小會自動根據不同的文字長度而自動調整。  
  
-   讓使用者輕鬆地將訊息標題、文字、按鈕文字和說明連結 (如果有的話) 複製到 [剪貼簿] 或是透過電子郵件訊息傳送這項資訊。  
  
-   當使用者按一下 [**其他資訊**] 時，顯示階層式關聯性樹狀結構中的所有基礎例外狀況和錯誤。  
  
-   讓使用者決定再次發生相同的例外狀況時，是否要顯示訊息。  
  
-   使用與例外狀況相關聯的說明連結來存取線上說明系統。  
  
 如需詳細資訊，請參閱[程式例外狀況訊息方塊](../../../2014/database-engine/dev-guide/program-exception-message-box.md)。  
  
  
