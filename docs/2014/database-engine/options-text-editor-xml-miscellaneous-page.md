---
title: 選項（文字編輯器-XML-其他頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 1a9509f0-c663-4b31-b396-7f5dc4371651
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: eb3422b859ce4e58fc05564357876c5fe09fcdff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089212"
---
# <a name="options-text-editor---xml---miscellaneous-page"></a>選項 (文字編輯器 - XML - 其他頁面)

[選項]**** 對話方塊，可以讓您變更 XML 編輯器的自動完成和結構描述設定。 在 [工具]**** 功能表上，按一下 [選項]****，展開 [文字編輯器]**** 資料夾，按一下 [XML]****，然後按一下 [其他]****，即可使用這些設定。  
  
## <a name="auto-insert"></a>自動插入  
 **結尾標記**  
 文字編輯器在撰寫 XML 元素時會加入結尾標記。 如果選取元素開始標記，編輯器會插入相符的結尾標記，包括相符的命名空間前置詞。 依預設，這個核取方塊為已選取。  
  
 **屬性引號**  
 撰寫 XML 屬性時，編輯器會插入 `="``"` 字元，並將插入號 (**^)** 置於引號內。 依預設，這個核取方塊為已選取。  
  
 **命名空間宣告**  
 編輯器在需要時會自動插入命名空間宣告。 依預設，這個核取方塊為已選取。  
  
 **其他標記 (註解、CDATA)**  
 註解、CDATA、DOCTYPE、處理指示，以及其他自動完成的標記。 依預設，這個核取方塊為已選取。  
  
## <a name="network"></a>網路  
 **自動下載 DTD 和結構描述**  
 結構描述和文件類型定義 (DTD) 會從 HTTP 位置自動下載。 此功能使用 System.Net 並啟用 Autoproxy 伺服器偵測。 依預設，這個核取方塊為已選取。  
  
## <a name="outlining"></a>大綱  
 **檔案開啟時進入大綱模式**  
 檔案開啟時啟動大綱功能。 依預設，這個核取方塊為已選取。  
  
## <a name="caching"></a>快取  
 **結構描述**  
 指定結構描述快取的位置。 瀏覽按鈕 (...) 會在新視窗中開啟目前的結構描述快取位置。 預設位置是* \<Management Studio 安裝目錄>* \xml\schemas。  
