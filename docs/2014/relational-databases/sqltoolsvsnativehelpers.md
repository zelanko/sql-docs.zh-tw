---
title: SqlToolsVSNativeHelpers | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: d33cb556-0380-490a-9220-b74062dbd6d9
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 98384288159ca4dea6dbd1f70deeb0be834c15a0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031396"
---
# <a name="sqltoolsvsnativehelpers"></a>SqlToolsVSNativeHelpers
  在 Visual Studio 中支援 SQL Server 功能的程式庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID /*lpReserved*/)  
```  
  
## <a name="return-value"></a>傳回值  
 如果 DLL 進入點正確初始化，則為布林值 `True`，否則為 `False`。  
  
## <a name="see-also"></a>另請參閱  
 [FrameWindowVisible](sqltoolsvsnativehelpers-framewindowvisible.md)  
  
  