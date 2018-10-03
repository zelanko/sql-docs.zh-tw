---
title: Visual c + + 的錯誤處理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e33d28201e1a2e4f7df8ac330ac89b3f00194b14
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630666"
---
# <a name="handling-errors-in-visual-c"></a>處理 Visual C++ 的錯誤
在 COM 中，大部分的作業會傳回 HRESULT 傳回碼指出函數是否已順利完成。 #Import 指示詞會產生每個 「 原始 」 的方法或屬性周圍的包裝函式程式碼，並檢查傳回的 HRESULT。 如果 HRESULT 指出失敗，包裝函式程式碼會擲回的 COM 錯誤的 HRESULT 傳回碼的呼叫 _com_issue_errorex() 做為引數。 COM 錯誤物件可以陷入**try / catch**區塊。 （為了效率的因素，攔截 _com_error 物件的參考）。  
  
 請記住，這些是 ADO 錯誤： 有人從 ADO 作業失敗。 基礎提供者所傳回的錯誤會顯示為**錯誤**中的物件**連線**物件的**錯誤**集合。  
  
 #Import 指示詞只會建立用於方法和屬性在 ADO.dll 中宣告的錯誤處理常式。 不過，您可以利用這個相同的錯誤處理機制撰寫您自己的錯誤檢查巨集或內嵌函式。 請參閱範例主題 C++® 延伸模組。
