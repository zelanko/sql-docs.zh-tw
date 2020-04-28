---
title: 設定 DCOM 資料流程封送處理格式 |Microsoft Docs
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
ms.openlocfilehash: 29bf8d19b9e3c9ec9b4072edd9575add9947c8f3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922211"
---
# <a name="setting-dcom-stream-marshaling-format"></a>設定 DCOM 資料流封送處理格式
使用 RDS 1.5 或更早版本之元件的用戶端電腦與使用 RDS 2.0 或更新版本之元件的伺服器不相容。 當使用 DCOM 做為基礎通訊協定時，RDS 2.0 或更新版本的支援會更有效率地傳輸[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 如果您的用戶端執行的是 RDS 1.5 或更早版本的元件，您可以將伺服器設定為與舊版 RDS 支援（稱為 RDS 1.0）或較新的 RDS 支援（稱為 RDS 2.0 或更新版本）搭配運作。 設定下列其中一個登錄專案：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -或-  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


