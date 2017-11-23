---
title: "錯誤 （Visual c + + 語法索引與 #import） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs: C++
helpviewer_keywords: 'Error collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 1ee59754-59c8-48e2-a4fb-242fa788c1f9
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c890b2d68f0ec22aae9c2a765839143bb8509fd6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="error-visual-c-syntax-index-with-import"></a>錯誤 （Visual c + + 語法索引與 #import）
## <a name="properties"></a>屬性  
  
```  
_bstr_t GetDescription( );  
__declspec(property(get=GetDescription)) _bstr_t Description;  
  
long GetHelpContext( );  
__declspec(property(get=GetHelpContext)) long HelpContext;  
  
_bstr_t GetHelpFile( );  
__declspec(property(get=GetHelpFile)) _bstr_t HelpFile;  
  
long GetNativeError( );  
__declspec(property(get=GetNativeError)) long NativeError;  
  
long GetNumber( );  
__declspec(property(get=GetNumber)) long Number;  
  
_bstr_t GetSource( );  
__declspec(property(get=GetSource)) _bstr_t Source;  
  
_bstr_t GetSQLState( );  
__declspec(property(get=GetSQLState)) _bstr_t SQLState;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)
