---
title: SqlToolsVSNativeHelpers | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: d33cb556-0380-490a-9220-b74062dbd6d9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 992f8288018fb248b14db13b2ed1104aeecab04d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63285572"
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
  
  
