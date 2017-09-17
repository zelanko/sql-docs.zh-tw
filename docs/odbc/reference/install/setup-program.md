---
title: "安裝程式 |Microsoft 文件"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 30637bacfb73d56528233ea13c4c6daeabecf814
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setup-program"></a>安裝程式
> **注意：**開頭為 Windows XP 和 Windows Server 2003、 **ODBC 隨附於 Windows 作業系統**。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 使用者執行安裝程式，以啟動安裝程序。 安裝程式會寫入應用程式或驅動程式的開發人員。 除了安裝 ODBC 元件，它可以安裝其他軟體。 例如，應用程式開發人員可能使用相同的安裝程式來安裝 ODBC 元件並安裝他們的應用程式。  
  
 開發人員可以撰寫安裝程式從從頭開始使用 Microsoft® Windows® SDK 安裝公用程式或其他廠商的安裝程式軟體。 這可讓這些開發人員完全控制安裝程式的外觀及操作。 若要安裝其他軟體，例如 ODBC 應用程式可以寫入安裝程式。 如需有關 Windows SDK 安裝公用程式的詳細資訊，請參閱 Windows SDK 的文件。  
  
 安裝中有多少實際上是由安裝程式，取決於哪些函數它的安裝程式 DLL 中呼叫。 安裝程式 DLL 包含函式來安裝個別的 ODBC 元件。 安裝程式只會呼叫**SQLInstallDriverManager**， **SQLInstallDriverEx**，或**SQLInstallTranslatorEx**在安裝程式中的 DLL，以便擷取的路徑目錄元件是安裝和元件的相關資訊新增至登錄。 這些函式不實際將複製檔案。安裝程式會使用這些函式的引數中的資訊。  
  
 安裝程式的 DLL 也包含用以移除 ODBC 元件函式。 安裝程式呼叫**SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator**在安裝程式中的計數遞減元件的使用方式的 DLL登錄和元件的新使用計數降至 0，如果從登錄移除所有元件的相關資訊。 這些函式不會移除元件; 的檔案安裝程式會如果新的使用計數降至 0。
