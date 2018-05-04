---
title: 設定 DCOM 資料流的封送處理格式 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eed72f16fa58e4dc47486967e615de746e27a2a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setting-dcom-stream-marshaling-format"></a>設定 DCOM 封送處理格式的資料流
使用元件從 RDS 1.5 或更早版本的用戶端電腦不相容於使用元件從 RDS 2.0 或更新版本的伺服器。 做為基礎的通訊協定使用 DCOM，RDS 2.0 或更新版本的支援時，更有效地進行傳輸[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 如果您的用戶端正在執行元件從 RDS 1.5 或更早版本，您可以設定您的伺服器以使用先前的 RDS 支援 （稱為 RDS 1.0） 或更新版本的 RDS 支援 (2.0 或更新版本呼叫 RDS)。 設定下列登錄項目之一：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -或-  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


