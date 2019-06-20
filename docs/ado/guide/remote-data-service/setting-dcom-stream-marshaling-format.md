---
title: 設定 DCOM Stream 封送處理格式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: adec8a50e6bcf0af25227e2e456f3f76692f6d67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704188"
---
# <a name="setting-dcom-stream-marshaling-format"></a>設定 DCOM 資料流封送處理格式
使用元件從 RDS 1.5 或更早版本的用戶端電腦不相容，使用從 RDS 2.0 或更新版本的元件與伺服器。 使用 DCOM 做為基礎的通訊協定，RDS 2.0 或更新版本的支援時，更有效地進行傳輸[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 如果您的用戶端正在執行從 RDS 1.5 或更早版本的元件，您可以設定您的伺服器以使用先前的 RDS 支援 （稱為 RDS 1.0） 或更新版本的 RDS 支援 (2.0 或更新版本呼叫 RDS)。 設定下列登錄項目：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -或-  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


